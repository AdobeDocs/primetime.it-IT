---
description: TVSDK fornisce elementi API che sono utili quando si implementano sospensioni attività, inclusi metodi, metadati e notifiche.
title: Elementi API di sospensione attività
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---

# Elementi API di sospensione attività {#blackout-api-elements}

TVSDK fornisce elementi API che sono utili quando si implementano sospensioni attività, inclusi metodi, metadati e notifiche.

Puoi utilizzare quanto segue durante l’implementazione di una soluzione di sospensione attività nel lettore.

* **PTMediaPlayer**

   * `registerCurrentItemAsBackgroundItem` Salva la risorsa caricata come risorsa di sfondo. Se `replaceCurrentItemWithPlayerItem` chiamato dopo questo metodo, TVSDK continua a scaricare il manifesto dell&#39;elemento in background fino a quando non chiami `unregisterCurrentBackgroundItem` , `stop`, o `reset` .

   * `unregisterCurrentBackgroundItem` Imposta l&#39;elemento di sfondo su zero e interrompe il recupero e l&#39;analisi del manifesto di sfondo.

* **PTMetadata.PTBlackoutMetadata** A `PTMetadata` classe specifica per le sospensioni attività.

  Questo consente di impostare intervalli non ricercabili (un array di `CMTimeRanges`) su TVSDK. TVSDK controlla questi intervalli ogni volta che l’utente cerca. Se è impostato e l’utente cerca in un intervallo non ricercabile, TVSDK forza il visualizzatore alla fine dell’intervallo non ricercabile.

* **INIZIA QUI DOPO** **PTAdMetadata** Abilita o disabilita il pre-roll su un flusso live impostando `enableLivePreroll` a YES o NO. Se NO, TVSDK non effettua una chiamata esplicita ad server per gli annunci pre-roll prima della riproduzione del contenuto e quindi non riproduce il pre-roll. Questo non ha alcun impatto sulle mid-roll. Il valore predefinito è YES.

* **NotificheNSN**

   * `PTTimedMetadataChangedInBackgroundNotification` - Pubblicato quando TVSDK rileva un tag sottoscritto nel manifesto in background e un nuovo `PTTimedMetadata` L&#39;istanza viene preparata da essa. L’oggetto della notifica è `PTMediaPlayerItem` istanza attualmente in riproduzione. Puoi recuperare `PTTimedMetadata` istanza dal file di notifica `userInfo` dizionario che utilizza `PTTimedMetadataKey` chiave.

   * `PTBackgroundManifestErrorNotification` - Pubblicato quando il lettore multimediale non riesce completamente a caricare il manifesto in background, ovvero tutti gli URL del flusso restituiscono un errore o una risposta non valida. L’oggetto della notifica è `PTMediaPlayerItem` istanza attualmente in riproduzione.

* **PTNotification**

   * `BACKGROUND_MANIFEST_WARNING`

      * Codice: 204000
      * Tipo: avvertenza
      * Errore nel download del manifesto in background.

   * `INVALID_SEEK_WARNING` Inviato quando si tenta una ricerca in un intervallo non ricercabile (in `nonSeekableRanges` imposta in `PTBlackoutMetadata`).
