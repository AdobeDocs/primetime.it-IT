---
description: La sezione di notifica della libreria TVSDK del browser consente di creare un sistema di registrazione e debug che può essere utile a scopo di diagnostica e convalida.
title: Sistema di notifica
exl-id: 6a3a3c56-1580-4f43-ba81-220a5b0fe5c3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# Sistema di notifica {#notification-system}

La sezione di notifica della libreria TVSDK del browser consente di creare un sistema di registrazione e debug che può essere utile a scopo di diagnostica e convalida.

<!--<a id="section_EC5DBE8DDA434B70A01FA2F3EF4618BD"></a>-->

Il TVSDK del browser dispone di un *nessun lancio* criterio per la relativa API. La maggior parte dei metodi restituisce un `PSDKErrorCode` valore per indicare se il metodo è stato eseguito correttamente. Per un elenco completo di tutti i possibili `PSDKErrorCode` , consulta Riferimenti dell&#39;API TVSDK del browser.

Gli errori asincroni vengono notificati tramite gli eventi specifici.

Invii TVSDK del browser `MediaPlayer` eventi per fornire informazioni sull’attività del lettore. Per acquisire e rispondere a tali eventi, è necessario implementare i listener di eventi.

>[!TIP]
>
>Gli eventi chiave e le informazioni vengono registrati nella console del browser web.

## Ascolta le notifiche {#section_06B96633433D497E842FB7ADD5F2C7DA}

Puoi ascoltare le notifiche e aggiungere le tue notifiche alla cronologia delle notifiche. Il nucleo del sistema di notifica TVSDK del browser è il `Notification` che rappresenta una notifica autonoma.

Per impostare l&#39;applicazione per l&#39;ascolto delle notifiche:

1. Ascolta le modifiche di stato di MediaPlayer tramite l’istanza MediaPlayer.

   ```js
   player.addEventListener( 
         AdobePSDK.PSDKEventType.STATUS_CHANGED, onStatusChange);
   ```

1. Implementa il callback.

   Il callback riceve un&#39;istanza del `AdobePSDK.MediaPlayerStatusChangeEvent`, e Browser TVSDK passa questo oggetto evento al callback che contiene il nuovo stato del lettore.
1. L&#39;applicazione può ascoltare altri eventi inviati dal TVSDK del browser utilizzando `MediaPlayer` dell&#39;istanza.
