---
description: TVSDK fornisce elementi API utili per l'implementazione delle blackout, inclusi metodi, metadati e notifiche.
seo-description: TVSDK fornisce elementi API utili per l'implementazione delle blackout, inclusi metodi, metadati e notifiche.
seo-title: Elementi API Blackout
title: Elementi API Blackout
uuid: ddc81558-4218-44d2-92df-15926c7c96b3
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 0%

---


# Elementi API Blackout{#blackout-api-elements}

TVSDK fornisce elementi API utili per l&#39;implementazione delle blackout, inclusi metodi, metadati e notifiche.

Quando si implementa una soluzione blackout nel lettore, è possibile utilizzare quanto segue.

* **PTMediaPlayer**

   * `registerCurrentItemAsBackgroundItem` Salva la risorsa attualmente caricata come risorsa in background. Se `replaceCurrentItemWithPlayerItem` viene chiamato dopo questo metodo, TVSDK continua a scaricare il manifesto dell&#39;elemento in background finché non invoca `unregisterCurrentBackgroundItem` , `stop` o `reset` .

   * `unregisterCurrentBackgroundItem` Imposta l&#39;elemento di sfondo su nil e interrompe il recupero e l&#39;analisi del manifesto di sfondo.

* **PTMetadata.** PTBlackoutMetadataUna  `PTMetadata` classe specifica per i blackout.

   Questo consente di impostare intervalli non ricercabili (un array di `CMTimeRanges`) in TVSDK. TVSDK controlla questi intervalli ogni volta che l&#39;utente cerca. Se è impostato e l’utente cerca in un intervallo non ricercabile, TVSDK forza il visualizzatore alla fine dell’intervallo non ricercabile.

* **START QUI** **** NEXTPTAdMetadataAbilitare o disabilitare il pre-roll su un flusso live impostando  `enableLivePreroll` su YES o NO. Se NO, TVSDK non effettua una chiamata ad-server esplicita per gli annunci pre-roll prima della riproduzione del contenuto, quindi non riproduce il pre-roll. Questo non ha alcun impatto sui rulli intermedi. Il valore predefinito è YES.

* **Notifiche NSN**

   * `PTTimedMetadataChangedInBackgroundNotification` - Pubblicato quando TVSDK rileva un tag con sottoscrizione nel manifesto di sfondo e ne prepara una nuova  `PTTimedMetadata` istanza. L&#39;oggetto della notifica è l&#39;istanza `PTMediaPlayerItem` attualmente in fase di riproduzione. È possibile recuperare l&#39;istanza `PTTimedMetadata` dal dizionario `userInfo` della notifica utilizzando la chiave `PTTimedMetadataKey`.

   * `PTBackgroundManifestErrorNotification` - Pubblicato quando il lettore multimediale non riesce completamente a caricare il manifesto di sfondo, ovvero tutti gli URL del flusso restituiscono un errore o una risposta non valida. L&#39;oggetto della notifica è l&#39;istanza `PTMediaPlayerItem` attualmente in fase di riproduzione.

* **PTNotificazione**

   * `BACKGROUND_MANIFEST_WARNING`

      * Codice: 204000
      * Tipo: Avviso
      * Errore nel download del manifesto in background.
   * `INVALID_SEEK_WARNING` Inviato quando un tentativo di ricerca viene eseguito in un intervallo non ricercabile ( `nonSeekableRanges` impostato in  `PTBlackoutMetadata`).


