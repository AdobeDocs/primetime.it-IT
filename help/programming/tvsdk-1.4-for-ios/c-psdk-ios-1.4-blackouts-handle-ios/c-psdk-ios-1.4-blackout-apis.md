---
description: TVSDK fornisce elementi API utili per l’implementazione delle blackout, inclusi metodi, metadati e notifiche.
title: Elementi dell’API Blackout
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---


# Elementi API di sospensione attività{#blackout-api-elements}

TVSDK fornisce elementi API utili per l’implementazione delle blackout, inclusi metodi, metadati e notifiche.

Quando si implementa una soluzione blackout nel lettore, è possibile utilizzare quanto segue.

* **PTMediaPlayer**

   * `registerCurrentItemAsBackgroundItem` Salva la risorsa attualmente caricata come risorsa in background. Se `replaceCurrentItemWithPlayerItem` viene chiamato dopo questo metodo, TVSDK continua a scaricare il manifesto dell&#39;elemento in background fino a quando non chiami `unregisterCurrentBackgroundItem` , `stop` o `reset` .

   * `unregisterCurrentBackgroundItem` Imposta l&#39;elemento di sfondo su nil e smette di recuperare e analizzare il manifesto di sfondo.

* **PTMetadata.** PTBlackoutMetadataUna  `PTMetadata` classe specifica per le blackout.

   Questo consente di impostare intervalli non ricercabili (una matrice di `CMTimeRanges`) su TVSDK. TVSDK controlla questi intervalli ogni volta che l’utente cerca. Se è impostato e l’utente cerca in un intervallo non ricercabile, TVSDK forza il visualizzatore alla fine dell’intervallo non ricercabile.

* **AVVIA QUI** **** NEXTPTAdMetadataAttiva o disattiva il pre-roll su un flusso live impostando  `enableLivePreroll` su YES o NO. Se NO, TVSDK non effettua una chiamata ad server esplicita per gli annunci pre-scorrimento prima della riproduzione del contenuto e quindi non riproduce il pre-roll. Questo non ha alcun impatto sui rulli medi. Il valore predefinito è YES.

* **Notifiche NSN**

   * `PTTimedMetadataChangedInBackgroundNotification` - Pubblicato quando TVSDK rileva un tag con sottoscrizione nel manifesto di background e ne prepara una nuova  `PTTimedMetadata` istanza. L&#39;oggetto della notifica è l&#39;istanza `PTMediaPlayerItem` attualmente in esecuzione. Puoi recuperare l’istanza `PTTimedMetadata` dal dizionario `userInfo` della notifica utilizzando la chiave `PTTimedMetadataKey` .

   * `PTBackgroundManifestErrorNotification` - Pubblicato quando il lettore multimediale non riesce completamente a caricare il manifesto in background, ovvero, tutti gli URL del flusso restituiscono un errore o una risposta non valida. L&#39;oggetto della notifica è l&#39;istanza `PTMediaPlayerItem` attualmente in esecuzione.

* **Notifica PTN**

   * `BACKGROUND_MANIFEST_WARNING`

      * Codice: 204000
      * Tipo: Avviso
      * Errore nel download del manifesto in background.
   * `INVALID_SEEK_WARNING` Inviato quando si tenta una ricerca in un intervallo non ricercabile (in  `nonSeekableRanges` impostato in  `PTBlackoutMetadata`).


