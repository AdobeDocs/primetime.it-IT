---
description: La parte di notifica della libreria Browser TVSDK consente di creare un sistema di registrazione e debug che può essere utile a scopo diagnostico e di convalida.
seo-description: La parte di notifica della libreria Browser TVSDK consente di creare un sistema di registrazione e debug che può essere utile a scopo diagnostico e di convalida.
seo-title: Sistema di notifica
title: Sistema di notifica
uuid: 69c4ff1d-3167-413b-ab49-942a5ddc34d7
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---


# Sistema di notifica {#notification-system}

La parte di notifica della libreria Browser TVSDK consente di creare un sistema di registrazione e debug che può essere utile a scopo diagnostico e di convalida.

<!--<a id="section_EC5DBE8DDA434B70A01FA2F3EF4618BD"></a>-->

Per l&#39;API del browser TVSDK è previsto un criterio *nessun&#39;azione*. La maggior parte dei metodi restituisce un valore `PSDKErrorCode` per indicare se il metodo è stato eseguito correttamente. Per un elenco completo di tutti i possibili valori `PSDKErrorCode`, consultate Riferimenti alle API TVSDK del browser.

Gli errori asincroni vengono notificati attraverso gli eventi specifici.

Il browser TVSDK invia eventi `MediaPlayer` per fornire informazioni sull&#39;attività del lettore. È necessario implementare i listener di eventi per acquisire e rispondere a tali eventi.

>[!TIP]
>
>Gli eventi e le informazioni chiave vengono registrati nella console del browser Web.

## Ascoltare le notifiche {#section_06B96633433D497E842FB7ADD5F2C7DA}

Potete ascoltare le notifiche e aggiungere notifiche personalizzate alla cronologia delle notifiche. Il nucleo del sistema di notifica TVSDK del browser è la classe `Notification`, che rappresenta una notifica indipendente.

Per impostare l&#39;applicazione in modo che ascolti le notifiche:

1. Ascoltare le modifiche dello stato di MediaPlayer utilizzando l’istanza MediaPlayer.

   ```js
   player.addEventListener( 
         AdobePSDK.PSDKEventType.STATUS_CHANGED, onStatusChange);
   ```

1. Implementa il callback.

   La callback riceve un&#39;istanza del `AdobePSDK.MediaPlayerStatusChangeEvent` e il browser TVSDK trasmette l&#39;oggetto evento al callback che contiene il nuovo stato del lettore.
1. L&#39;applicazione può ascoltare altri eventi inviati da Browser TVSDK utilizzando l&#39;istanza `MediaPlayer`.

