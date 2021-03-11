---
description: I gestori di eventi consentono al browser TVSDK di rispondere agli eventi.
title: Implementare listener e callback di eventi
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 1%

---


# Implementa listener di eventi e callback{#implement-event-listeners-and-callbacks}

I gestori di eventi consentono al browser TVSDK di rispondere agli eventi.

Quando si verifica un evento, il meccanismo eventi del browser TVSDK chiama il gestore eventi registrato e trasmette le informazioni sull&#39;evento al gestore.

L&#39;applicazione deve implementare listener di eventi per gli eventi TVSDK del browser che influiscono sull&#39;applicazione.

1. Determinare gli eventi che l&#39;applicazione deve ascoltare.

   * **Eventi** richiesti: Ascoltare tutti gli eventi di riproduzione.

      >[!IMPORTANT]
      >
      >L&#39;evento di riproduzione `STATUS_CHANGED` fornisce lo stato del lettore, compresi gli errori. Uno qualsiasi degli stati potrebbe influenzare il passaggio successivo del lettore.

   * **Altri eventi**: Facoltativo, a seconda dell’applicazione.

      Ad esempio, se incorpori pubblicità nella riproduzione, ascolta tutti gli eventi `AdBreakPlaybackEvent` e `AdPlaybackEvent`.

1. Implementa i listener di eventi per ogni evento.

   Il browser TVSDK restituisce i valori dei parametri alle chiamate di ritorno del listener di eventi. Questi valori forniscono informazioni rilevanti sull&#39;evento che è possibile utilizzare nei listener per eseguire le azioni appropriate.

   Ad esempio:

   * Tipo evento: `AdobePSDK.PSDKEventType.STATUS_CHANGED`
   * Proprietà evento: `MediaPlayerStatus.<event>` utilizzato in questo modo:

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

1. Registra i listener di callback con l&#39;oggetto `MediaPlayer` utilizzando `MediaPlayer.addEventListener`.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED,  
                                    onStatusChange);
   ```
