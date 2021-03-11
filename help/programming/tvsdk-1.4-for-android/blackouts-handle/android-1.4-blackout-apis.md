---
description: È possibile gestire i blackout nei flussi video in diretta e fornire contenuti alternativi durante una sospensione attività.
title: Elementi dell’API Blackout
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 0%

---


# Elementi API di sospensione attività{#blackout-api-elements}

È possibile gestire i blackout nei flussi video in diretta e fornire contenuti alternativi durante una sospensione attività.

Quando si verifica un blackout in un flusso live, il lettore utilizza gestori eventi per rilevare la blackout e fornire contenuti alternativi agli utenti che non sono idonei a guardare il flusso principale. Il lettore rileva l&#39;inizio e la fine del periodo di sospensione attività, passa la riproduzione dal flusso principale a un flusso alternativo e torna al flusso principale al termine del periodo di sospensione attività.

Per gestire i blackout nei flussi live:

1. Imposta l’app per rilevare i tag di blackout mediante l’iscrizione ai tag di blackout in un manifesto in streaming live.

   TVSDK non rileva i tag di blackout da solo; devi abbonarti ai tag di blackout per ricevere la notifica quando i tag vengono rilevati durante l’analisi dei file manifest.
1. Crea listener di eventi per i tag a cui il lettore è iscritto (in questo caso, i tag PLAYBACK e BLACKOUTS) .

   Quando si verifica un tag a cui il lettore ha effettuato la sottoscrizione (ad esempio, un tag blackout) in primo piano (contenuto principale) o in background (contenuto alternativo), il TVSDK invia un `TimedMetadataEvent` e crea un `TimedMetadataObject` per il `TimedMetadataEvent`.

1. Implementa i gestori per gli eventi di metadati temporizzati sia per i flussi in primo piano che per quelli in background.

   In questi gestori, ottieni gli orari di inizio e fine del periodo di sospensione attività dagli oggetti evento metadati temporizzati.
1. Crea metodi per cambiare contenuto all’inizio e alla fine del periodo di sospensione attività.

   All’avvio del periodo di sospensione attività, sposta il contenuto principale in background e cambia il contenuto alternativo in modo che diventi il flusso principale. Continua a recuperare e analizzare il manifesto originale in background e continua a controllare il tag &quot;blackout end end&quot;, in modo che il lettore possa ricongiungersi al flusso originale al termine del blackout.
1. Aggiornare gli intervalli non ricercabili se l&#39;intervallo di blackout è in DVR sul flusso di riproduzione.

   Tieni traccia e gestisci i `TimedMetadata` nel flusso di background, preparando e aggiornando intervalli non ricercabili di blackout.

TVSDK fornisce elementi API utili per l’implementazione delle blackout, inclusi metodi, metadati e notifiche.

Quando si implementa una soluzione blackout nel lettore, è possibile utilizzare quanto segue.

* **MediaPlayer**

   * `registerCurrentItemAsBackgroundItem` Salva la risorsa attualmente caricata come risorsa in background. Se `replaceCurrentResource` viene chiamato dopo questo metodo, TVSDK continua a scaricare il manifesto dell&#39;elemento in background fino a quando non chiami `unregisterCurrentBackgroundItem`, `release` o `reset`.

   * `unregisterCurrentBackgroundItem` Imposta l&#39;elemento di sfondo su null e interrompe il recupero e l&#39;analisi del manifesto di sfondo.

* **BlackoutMetadata**  -

   Classe Metadata specifica per le blackout.

   Questo consente di impostare intervalli non ricercabili (una matrice di `TimeRanges`) su TVSDK. TVSDK controlla questi intervalli ogni volta che l’utente cerca. Se è impostato e l’utente cerca in un intervallo non ricercabile, TVSDK forza il visualizzatore alla fine dell’intervallo non ricercabile.

* **INIZIA QUI SUCCESSIVO** AdvertisingMetadataAttiva o disattiva il preroll su un flusso live impostando  `enableLivePreroll` su true o false. Se false, TVSDK non effettua una chiamata ad server esplicita per gli annunci pre-scorrimento prima della riproduzione del contenuto, e quindi non riproduce il pre-roll. Questo non ha alcun impatto sui rulli medi. Il valore predefinito è true.

* **MediaPlayer.BlackoutsEventListener**

   * `onTimedMetadataInBackgroundItem` - Inviato quando rileva un tag di sottoscrizione nel manifesto di background e ne viene preparata una nuova  `TimedMetadata` istanza. L&#39;istanza `TimedMetadata` viene inviata come parametro.

   * `onBackgroundManifestFailed` - Inviato quando il lettore multimediale non riesce completamente a caricare il manifesto in background, ovvero tutti gli URL del flusso restituiscono un errore o una risposta non valida.

* **Notifiche**

   * `BACKGROUND_MANIFEST_WARNING`

      * Codice: 204000
      * Tipo: Avviso
      * Errore nel download del manifesto in background.