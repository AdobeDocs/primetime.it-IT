---
description: Prima di poter utilizzare la maggior parte dei metodi del lettore TVSDK del browser, il lettore deve trovarsi in uno stato valido.
title: Attendi uno stato valido
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 0%

---


# Attendi uno stato valido {#wait-for-a-valid-state}

Prima di poter utilizzare la maggior parte dei metodi del lettore TVSDK del browser, il lettore deve trovarsi in uno stato valido.

Il lettore passa attraverso vari stati. In attesa che il lettore sia nello stato corretto, la risorsa multimediale viene caricata correttamente. Se il lettore non è almeno nello stato richiesto, molti metodi di riproduzione generano `IllegalStateException`.

In genere lo stato richiesto è PREPARATO.

1. Per confermare che lo stato è PREPARATO:

   Quando il lettore sta inizializzando, attendi che il browser TVSDK invii l&#39;evento `AdobePSDK.MediaPlayerStatusChangeEvent` con un `event.status` di `MediaPlayerStatus.PREPARED`.

   Verificare se lo stato corrente dell&#39;oggetto MediaPlayer è almeno PREPARATO.

   ```
   <readonly> status :AdobePSDK.MediaPlayerStatus
   ```

