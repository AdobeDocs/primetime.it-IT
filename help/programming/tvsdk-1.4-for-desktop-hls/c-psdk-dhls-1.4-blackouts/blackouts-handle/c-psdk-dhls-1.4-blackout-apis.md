---
description: TVSDK fornisce elementi API che sono utili quando si implementano sospensioni attività, inclusi metodi, metadati e notifiche.
title: Elementi API di sospensione attività
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---

# Elementi API di sospensione attività{#blackout-api-elements}

TVSDK fornisce elementi API che sono utili quando si implementano sospensioni attività, inclusi metodi, metadati e notifiche.

Puoi utilizzare quanto segue durante l’implementazione di una soluzione di sospensione attività nel lettore.

* **MediaPlayer**

   * `registerCurrentItemAsBackgroundItem` Salva la risorsa caricata come risorsa di sfondo. Se `replaceCurrentResource` chiamato dopo questo metodo, TVSDK continua a scaricare il manifesto dell&#39;elemento in background fino a quando non chiami `unregisterCurrentBackgroundItem`.

   * `unregisterCurrentBackgroundItem`  Cancella la risorsa di sfondo attualmente impostata e interrompe il recupero e l&#39;analisi del manifesto di sfondo.

* **MetadatiSospensione attività** Tipo di metadati specifico per le sospensioni attività.

  Questo consente di impostare intervalli non ricercabili (un `TimeRange` attributo chiamato `nonseekableRange`) su TVSDK. TVSDK controlla questi intervalli (se la posizione di ricerca desiderata rientra in un `nonseekableRange`) ogni volta che l’utente cerca. Se è impostato e l’utente cerca in un intervallo non ricercabile, TVSDK forza il visualizzatore all’ora di fine del `seekableRange`.

* **INIZIA QUI DOPO** **DefaultMetadataKeys** Abilita o disabilita la funzione di preroll su un flusso live impostando `ENABLE_LIVE_PREROLL` su true o false. Se false, TVSDK non effettua una chiamata esplicita al server degli annunci pre-roll prima della riproduzione del contenuto e quindi non riproduce il pre-roll. Questo non ha alcun impatto sulle mid-roll. Il valore predefinito è true.

* **TimedMetadataEvent**

   * `TIMED_METADATA_IN_BACKGROUND_AVAILABLE` sottotipo evento: inviato quando TVSDK rileva un tag sottoscritto nel manifesto in background.

* **Notifiche**

   * `BACKGROUND_MANIFEST_WARNING`

      * Codice: 204000
      * Tipo: avvertenza
      * Errore nel download del manifesto in background.

   * `SeekEvent.SEEK_POSITION_ADJUSTED` Inviato quando si tenta una ricerca in un intervallo non ricercabile.
