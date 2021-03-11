---
description: TVSDK fornisce elementi API utili per l’implementazione delle blackout, inclusi metodi, metadati e notifiche.
title: Elementi dell’API Blackout
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---


# Elementi API di sospensione attività{#blackout-api-elements}

TVSDK fornisce elementi API utili per l’implementazione delle blackout, inclusi metodi, metadati e notifiche.

Quando si implementa una soluzione blackout nel lettore, è possibile utilizzare quanto segue.

* **MediaPlayer**

   * `registerCurrentItemAsBackgroundItem` Salva la risorsa attualmente caricata come risorsa in background. Se `replaceCurrentResource` viene chiamato dopo questo metodo, TVSDK continua a scaricare il manifesto dell&#39;elemento in background fino a quando non chiami `unregisterCurrentBackgroundItem`.

   * `unregisterCurrentBackgroundItem`  Cancella la risorsa in background attualmente impostata e interrompe il recupero e l&#39;analisi del manifesto in background.

* **** BlackoutMetadataUn tipo di metadati specifico per le blackout.

   Questo consente di impostare intervalli non ricercabili (un attributo aggiuntivo `TimeRange` denominato `nonseekableRange`) su TVSDK. TVSDK controlla questi intervalli (se la posizione di ricerca desiderata rientra in un `nonseekableRange`) ogni volta che l’utente cerca. Se è impostato e l’utente cerca in un intervallo non ricercabile, TVSDK forza il visualizzatore all’ora di fine del `seekableRange`.

* **AVVIA QUI** **** NEXTDefaultMetadataKeysAttiva o disattiva la preroll su un flusso live impostando  `ENABLE_LIVE_PREROLL` su true o false. Se false, TVSDK non effettua una chiamata ad server esplicita per gli annunci pre-scorrimento prima della riproduzione del contenuto, e quindi non riproduce il pre-roll. Questo non ha alcun impatto sui rulli medi. Il valore predefinito è true.

* **TimedMetadataEvent**

   * `TIMED_METADATA_IN_BACKGROUND_AVAILABLE` sottotipo evento : inviato quando TVSDK rileva un tag con sottoscrizione nel manifesto di background.

* **Notifiche**

   * `BACKGROUND_MANIFEST_WARNING`

      * Codice: 204000
      * Tipo: Avviso
      * Errore nel download del manifesto in background.
   * `SeekEvent.SEEK_POSITION_ADJUSTED` Inviato quando si tenta una ricerca in un intervallo non ricercabile.


