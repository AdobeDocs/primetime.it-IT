---
description: La porzione di notifica della libreria TVSDK del browser consente di creare un sistema di registrazione e debug che può essere utile a scopo diagnostico e di convalida.
title: Sistema di notifica
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---


# Sistema di notifica {#notification-system}

La porzione di notifica della libreria TVSDK del browser consente di creare un sistema di registrazione e debug che può essere utile a scopo diagnostico e di convalida.

<!--<a id="section_EC5DBE8DDA434B70A01FA2F3EF4618BD"></a>-->

Il browser TVSDK dispone di un criterio *nessun pull* per la relativa API. La maggior parte dei metodi restituisce un valore `PSDKErrorCode` per indicare se il metodo è stato eseguito correttamente. Per un elenco completo di tutti i possibili valori `PSDKErrorCode`, consulta Riferimenti API TVSDK per browser .

Gli errori asincroni vengono notificati tramite gli eventi specifici.

Il browser TVSDK invia eventi `MediaPlayer` per fornire informazioni sull’attività del lettore. È necessario implementare i listener di eventi per acquisire e rispondere a tali eventi.

>[!TIP]
>
>Gli eventi e le informazioni chiave sono registrati nella console del browser Web.

## Ascolta le notifiche {#section_06B96633433D497E842FB7ADD5F2C7DA}

Puoi ascoltare le notifiche e aggiungere le tue notifiche alla cronologia delle notifiche. Il nucleo del sistema di notifica TVSDK per browser è la classe `Notification` che rappresenta una notifica autonoma.

Per impostare l&#39;applicazione in modo che ascolti le notifiche:

1. Ascoltare le modifiche dello stato di MediaPlayer utilizzando l&#39;istanza MediaPlayer.

   ```js
   player.addEventListener( 
         AdobePSDK.PSDKEventType.STATUS_CHANGED, onStatusChange);
   ```

1. Implementa il callback.

   Il callback riceve un&#39;istanza del `AdobePSDK.MediaPlayerStatusChangeEvent` e il browser TVSDK passa questo oggetto evento al callback che contiene il nuovo stato del lettore.
1. L&#39;applicazione può ascoltare altri eventi inviati dal browser TVSDK utilizzando l&#39;istanza `MediaPlayer` .

