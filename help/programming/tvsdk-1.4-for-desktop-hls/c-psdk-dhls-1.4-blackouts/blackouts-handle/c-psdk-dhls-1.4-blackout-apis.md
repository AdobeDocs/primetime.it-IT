---
description: TVSDK fornisce elementi API utili per l'implementazione delle blackout, inclusi metodi, metadati e notifiche.
seo-description: TVSDK fornisce elementi API utili per l'implementazione delle blackout, inclusi metodi, metadati e notifiche.
seo-title: Elementi API Blackout
title: Elementi API Blackout
uuid: 65e1668c-6a19-4910-83a2-46d364e94e5f
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---


# Elementi API Blackout{#blackout-api-elements}

TVSDK fornisce elementi API utili per l&#39;implementazione delle blackout, inclusi metodi, metadati e notifiche.

Quando si implementa una soluzione blackout nel lettore, è possibile utilizzare quanto segue.

* **MediaPlayer**

   * `registerCurrentItemAsBackgroundItem` Salva la risorsa attualmente caricata come risorsa in background. Se `replaceCurrentResource` viene chiamato dopo questo metodo, TVSDK continua a scaricare il manifesto dell&#39;elemento in background finché non chiami `unregisterCurrentBackgroundItem`.

   * `unregisterCurrentBackgroundItem`  Cancella la risorsa di sfondo attualmente impostata e interrompe il recupero e l&#39;analisi del manifesto di sfondo.

* **** BlackoutMetadataUn tipo di metadati specifico per i blackout.

   Questo consente di impostare intervalli non ricercabili (un attributo aggiuntivo `TimeRange` denominato `nonseekableRange`) in TVSDK. TVSDK controlla questi intervalli (se la posizione di ricerca desiderata rientra in un `nonseekableRange`) ogni volta che l&#39;utente cerca. Se è impostato e l’utente cerca in un intervallo non ricercabile, TVSDK forza il visualizzatore all’ora di fine del `seekableRange`.

* **START HERE** **** NEXTDefaultMetadataKeysAbilitare o disabilitare il preroll su un flusso live impostando  `ENABLE_LIVE_PREROLL` su true o false. Se è false, TVSDK non esegue una chiamata ad un server per annunci pre-roll prima della riproduzione del contenuto, pertanto non riproduce il pre-roll. Questo non ha alcun impatto sui rulli intermedi. Il valore predefinito è true.

* **TimedMetadataEvent**

   * `TIMED_METADATA_IN_BACKGROUND_AVAILABLE` sottotipo evento - Inviato quando TVSDK rileva un tag con sottoscrizione nel manifesto di sfondo.

* **Notifiche**

   * `BACKGROUND_MANIFEST_WARNING`

      * Codice: 204000
      * Tipo: Avviso
      * Errore nel download del manifesto in background.
   * `SeekEvent.SEEK_POSITION_ADJUSTED` Inviato quando si tenta di eseguire una ricerca in un intervallo non ricercabile.


