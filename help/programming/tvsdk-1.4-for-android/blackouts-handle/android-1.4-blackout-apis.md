---
description: È possibile gestire le sospensioni attività nei flussi video live e fornire contenuto alternativo durante una sospensione attività.
title: Elementi API di sospensione attività
exl-id: 8e4f1dc3-f2f6-4db9-b9d0-3e79d21032e9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 0%

---

# Elementi API di sospensione attività{#blackout-api-elements}

È possibile gestire le sospensioni attività nei flussi video live e fornire contenuto alternativo durante una sospensione attività.

Quando si verifica una sospensione attività in un flusso live, il lettore utilizza gestori di eventi per rilevare la sospensione attività e fornire contenuto alternativo agli utenti non idonei a guardare il flusso principale. Il lettore rileva l&#39;inizio e la fine del periodo di sospensione attività, passa la riproduzione dal flusso principale a un flusso alternativo e torna al flusso principale al termine del periodo di sospensione attività.

Per gestire le sospensioni attività nei flussi live:

1. Imposta l&#39;app per rilevare i tag di sospensione attività mediante l&#39;iscrizione a tali tag in un manifesto live-stream.

   TVSDK non rileva i tag di sospensione attività da solo. È necessario sottoscrivere i tag di sospensione attività per ricevere una notifica quando i tag vengono rilevati durante l&#39;analisi del file manifesto.
1. Crea listener di eventi per i tag a cui il lettore è abbonato (in questo caso, tag PLAYBACK e BLACKOUT).

   Quando si verifica un tag a cui il lettore si è abbonato (ad esempio, un tag di sospensione attività) nei manifesti di flusso in primo piano (contenuto principale) o in background (contenuto alternativo), TVSDK invia un tag `TimedMetadataEvent` e crea un `TimedMetadataObject` per `TimedMetadataEvent`.

1. Implementa gestori per gli eventi di metadati temporizzati per i flussi in primo piano e in background.

   In questi gestori, ottenere gli orari di inizio e fine per il periodo di sospensione attività dagli oggetti evento metadati temporizzati.
1. Creare metodi per cambiare il contenuto all&#39;inizio e alla fine del periodo di sospensione attività.

   All&#39;avvio del periodo di sospensione attività, passa il contenuto principale allo sfondo e cambia il contenuto alternativo in flusso principale. Continua a recuperare e analizzare il manifesto originale in background e continua a verificare la presenza del tag &quot;blackout end&quot;, in modo che il lettore possa unirsi nuovamente al flusso originale al termine della blackout.
1. Aggiornare gli intervalli non ricercabili se l&#39;intervallo di sospensione attività è in DVR nel flusso di riproduzione.

   Tracciare e gestire `TimedMetadata` nel flusso in background, preparando e aggiornando intervalli non ricercabili di sospensione attività.

TVSDK fornisce elementi API che sono utili quando si implementano sospensioni attività, inclusi metodi, metadati e notifiche.

Puoi utilizzare quanto segue durante l’implementazione di una soluzione di sospensione attività nel lettore.

* **MediaPlayer**

   * `registerCurrentItemAsBackgroundItem` Salva la risorsa caricata come risorsa di sfondo. Se `replaceCurrentResource` chiamato dopo questo metodo, TVSDK continua a scaricare il manifesto dell&#39;elemento in background fino a quando non chiami `unregisterCurrentBackgroundItem`, `release`, o `reset`.

   * `unregisterCurrentBackgroundItem` Imposta l&#39;elemento in background su null e interrompe il recupero e l&#39;analisi del manifesto in background.

* **MetadatiSospensione attività** -

   Classe di metadati specifica per le sospensioni attività.

   Questo consente di impostare intervalli non ricercabili (un array di `TimeRanges`) su TVSDK. TVSDK controlla questi intervalli ogni volta che l’utente cerca. Se è impostato e l’utente cerca in un intervallo non ricercabile, TVSDK forza il visualizzatore alla fine dell’intervallo non ricercabile.

* **INIZIA QUI IL PROSSIMO AdvertisingMetadata** Abilita o disabilita la funzione di preroll su un flusso live impostando `enableLivePreroll` su true o false. Se false, TVSDK non effettua una chiamata esplicita al server degli annunci pre-roll prima della riproduzione del contenuto e quindi non riproduce il pre-roll. Questo non ha alcun impatto sulle mid-roll. Il valore predefinito è true.

* **MediaPlayer.BlackoutsEventListener**

   * `onTimedMetadataInBackgroundItem` : inviato quando rileva un tag sottoscritto nel manifesto in background e un nuovo `TimedMetadata` L&#39;istanza viene preparata da essa. Il `TimedMetadata` l’istanza viene inviata come parametro.

   * `onBackgroundManifestFailed` - Inviato quando il lettore multimediale non riesce completamente a caricare il manifesto in background, ovvero tutti gli URL del flusso restituiscono un errore o una risposta non valida.

* **Notifiche**

   * `BACKGROUND_MANIFEST_WARNING`

      * Codice: 204000
      * Tipo: avvertenza
      * Errore nel download del manifesto in background.
