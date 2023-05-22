---
description: I gestori di eventi consentono a TVSDK del browser di rispondere agli eventi.
title: Implementare listener di eventi e callback
exl-id: 2ab33c03-4df6-48e5-825c-95aeef8855d2
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 0%

---

# Implementare listener di eventi e callback{#implement-event-listeners-and-callbacks}

I gestori di eventi consentono a TVSDK del browser di rispondere agli eventi.

Quando si verifica un evento, il meccanismo di evento del TVSDK del browser chiama il gestore eventi registrato e trasmette le informazioni sull’evento al gestore.

L&#39;applicazione deve implementare listener di eventi per gli eventi TVSDK del browser che influiscono sull&#39;applicazione.

1. Determina per quali eventi l&#39;applicazione deve essere in ascolto.

   * **Eventi richiesti**: ascolta tutti gli eventi di riproduzione.

      >[!IMPORTANT]
      >
      >Evento di riproduzione `STATUS_CHANGED` fornisce lo stato del lettore, compresi gli errori. Uno qualsiasi degli stati potrebbe influire sul passaggio successivo del lettore.

   * **Altri eventi**: facoltativo, a seconda dell’applicazione.

      Ad esempio, se incorpori pubblicità nella riproduzione, ascolta per tutti `AdBreakPlaybackEvent` e `AdPlaybackEvent` eventi.

1. Implementa listener di eventi per ogni evento.

   Il TVSDK del browser restituisce i valori dei parametri ai callback del listener di eventi. Questi valori forniscono informazioni rilevanti sull&#39;evento che è possibile utilizzare nei listener per eseguire azioni appropriate.

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

1. Registrare i listener di callback con `MediaPlayer` oggetto utilizzando `MediaPlayer.addEventListener`.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED,  
                                    onStatusChange);
   ```
