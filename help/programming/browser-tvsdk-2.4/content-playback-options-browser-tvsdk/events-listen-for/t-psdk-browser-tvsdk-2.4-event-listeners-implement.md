---
description: I gestori di eventi consentono al browser TVSDK di rispondere agli eventi.
seo-description: I gestori di eventi consentono al browser TVSDK di rispondere agli eventi.
seo-title: Implementare listener e callback di eventi
title: Implementare listener e callback di eventi
uuid: 63f62c60-505e-4f83-bc0d-58895d85a75a
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Implementare listener e callback di eventi{#implement-event-listeners-and-callbacks}

I gestori di eventi consentono al browser TVSDK di rispondere agli eventi.

Quando si verifica un evento, il meccanismo eventi del browser TVSDK chiama il gestore eventi registrato e trasmette le informazioni sull&#39;evento al gestore.

L&#39;applicazione deve implementare i listener di eventi per gli eventi TVSDK del browser che interessano l&#39;applicazione.

1. Determinare gli eventi che l&#39;applicazione deve ascoltare.

   * **Eventi** richiesti: Ascoltare tutti gli eventi di riproduzione.

      >[!IMPORTANT]
      >
      >L&#39;evento di riproduzione `STATUS_CHANGED` fornisce lo stato del lettore, inclusi gli errori. Uno qualsiasi degli stati potrebbe influenzare il prossimo passo del giocatore.

   * **Altri eventi**: Facoltativo, a seconda dell’applicazione in uso.

      Ad esempio, se si incorpora della pubblicità nella riproduzione, è possibile ascoltare tutti `AdBreakPlaybackEvent` gli `AdPlaybackEvent` eventi e gli eventi.

1. Implementare i listener di eventi per ogni evento.

   Il browser TVSDK restituisce i valori dei parametri alle callback del listener di eventi. Questi valori forniscono informazioni rilevanti sull&#39;evento che è possibile utilizzare nei listener per eseguire le azioni appropriate.

   Ad esempio:

   * Tipo evento: `AdobePSDK.PSDKEventType.STATUS_CHANGED`
   * Proprietà Event: utilizzato `MediaPlayerStatus.<event>` come segue:

```js
player.addEventListener( 
            AdobePSDK.PSDKEventType.STATUS_CHANGED,  
            onStatusChange); 
 
onStatusChange = function (event) { 
 
    switch (event.status) { 
        case AdobePSDK.MediaPlayerStatus.IDLE: 
            console.log("Player Status: IDLE"); 
            break;
```

1. Registra i listener di callback con l&#39; `MediaPlayer` oggetto utilizzando `MediaPlayer.addEventListener`.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED,  
                                    onStatusChange);
   ```
