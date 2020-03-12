---
description: Potete gestire i blackout nei flussi video live e fornire contenuto alternativo durante un blackout.
seo-description: Potete gestire i blackout nei flussi video live e fornire contenuto alternativo durante un blackout.
seo-title: Elementi API Blackout
title: Elementi API Blackout
uuid: 263a8987-0c85-493a-9352-9605c877ba65
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Elementi API Blackout{#blackout-api-elements}

Potete gestire i blackout nei flussi video live e fornire contenuto alternativo durante un blackout.

Quando si verifica un blackout in un flusso live, il lettore utilizza i gestori eventi per rilevare il blackout e fornire contenuto alternativo agli utenti non idonei a guardare il flusso principale. Il lettore rileva l&#39;inizio e la fine del periodo di blackout, passa la riproduzione dal flusso principale a un flusso alternativo e ritorna al flusso principale al termine del periodo di blackout.

Per gestire i blackout nei flussi live:

1. Configurate l&#39;app per rilevare i tag di blackout iscrivendosi ai tag di blackout in un manifesto in streaming live.

   TVSDK non rileva tag blackout autonomamente; per ricevere la notifica quando i tag vengono rilevati durante l&#39;analisi del file manifesto, dovete abbonarvi ai tag blackout.
1. Creare listener di eventi per i tag sottoscritti dal lettore (in questo caso, i tag PLAYBACK e BLACKOUTS).

   Quando si verifica un tag a cui il lettore ha effettuato la sottoscrizione (ad esempio, un tag blackout) nei manifesti del flusso in primo piano (contenuto principale) o in background (contenuto alternativo), TVSDK invia un `TimedMetadataEvent` e crea un `TimedMetadataObject` nome per il `TimedMetadataEvent`.

1. Implementate i gestori per gli eventi di metadati temporizzati per i flussi in primo piano e in background.

   In questi gestori, ottenete l&#39;ora di inizio e di fine del periodo di sospensione dagli oggetti evento metadati temporizzati.
1. Creare metodi per cambiare il contenuto all’inizio e alla fine del periodo di sospensione attività.

   All&#39;avvio del periodo di sospensione attività, passate il contenuto principale allo sfondo e passate il contenuto alternativo in modo che diventi il flusso principale. Continuare a recuperare e analizzare il manifesto originale in background e continuare a controllare il tag &quot;blackout end end&quot;, in modo che il lettore possa rientrare nel flusso originale al termine del blackout.
1. Aggiornate gli intervalli non ricercabili se l&#39;intervallo di blackout è in DVR sul flusso di riproduzione.

   Tenere traccia e gestire il flusso `TimedMetadata` in background, preparando e aggiornando gli intervalli non ricercabili del blackout.

TVSDK fornisce elementi API utili per l&#39;implementazione delle blackout, inclusi metodi, metadati e notifiche.

Quando si implementa una soluzione blackout nel lettore, è possibile utilizzare quanto segue.

* **MediaPlayer**

   * `registerCurrentItemAsBackgroundItem` Salva la risorsa attualmente caricata come risorsa in background. Se `replaceCurrentResource` viene chiamato dopo questo metodo, TVSDK continua a scaricare il manifesto dell&#39;elemento in background finché non invoca `unregisterCurrentBackgroundItem`, `release`o `reset`.

   * `unregisterCurrentBackgroundItem` Imposta l&#39;elemento di sfondo su null e interrompe il recupero e l&#39;analisi del manifesto di sfondo.

* **BlackoutMetadata** -

   Una classe di metadati specifica per i blackout.

   Questo consente di impostare intervalli non ricercabili (un array di `TimeRanges`) su TVSDK. TVSDK controlla questi intervalli ogni volta che l&#39;utente cerca. Se è impostato e l’utente cerca in un intervallo non ricercabile, TVSDK forza il visualizzatore alla fine dell’intervallo non ricercabile.

* **AVVIA QUI SUCCESSIVO AnnuncioMetadati** Attiva o disattiva il preroll su un flusso live impostando `enableLivePreroll` su true o false. Se è false, TVSDK non effettua una chiamata ad-server esplicita per gli annunci pre-roll prima della riproduzione del contenuto, quindi non riproduce il pre-roll. Questo non ha alcun impatto sui rulli intermedi. Il valore predefinito è true.

* **MediaPlayer.BlackoutsEventListener**

   * `onTimedMetadataInBackgroundItem` - Inviato quando rileva un tag con sottoscrizione nel manifesto di sfondo e ne prepara una nuova `TimedMetadata` istanza. L’ `TimedMetadata` istanza viene inviata come parametro.

   * `onBackgroundManifestFailed` - Inviato quando il lettore multimediale non riesce completamente a caricare il manifesto di sfondo, ovvero tutti gli URL del flusso restituiscono un errore o una risposta non valida.

* **Notifiche**

   * `BACKGROUND_MANIFEST_WARNING`

      * Codice: 204000
      * Tipo: Avviso
      * Errore nel download del manifesto in background.