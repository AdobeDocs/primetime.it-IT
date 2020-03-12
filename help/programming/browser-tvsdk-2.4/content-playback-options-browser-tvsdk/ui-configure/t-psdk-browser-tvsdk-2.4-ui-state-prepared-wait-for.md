---
description: Per poter utilizzare la maggior parte dei metodi del lettore TVSDK del browser, il lettore deve trovarsi in uno stato valido.
seo-description: Per poter utilizzare la maggior parte dei metodi del lettore TVSDK del browser, il lettore deve trovarsi in uno stato valido.
seo-title: Attendere uno stato valido
title: Attendere uno stato valido
uuid: 0add29a8-fbd8-483a-8c99-e4bc6de9e3d3
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Attendere uno stato valido {#wait-for-a-valid-state}

Per poter utilizzare la maggior parte dei metodi del lettore TVSDK del browser, il lettore deve trovarsi in uno stato valido.

Il lettore si sposta attraverso vari stati. In attesa che il lettore sia nello stato corretto, la risorsa multimediale viene caricata correttamente. Se il lettore non è almeno nello stato richiesto, vengono lanciati molti metodi `IllegalStateException`.

In genere lo stato richiesto è PREPARATO.

1. Per confermare che lo stato è PREPARATO:

   Quando il lettore è in fase di inizializzazione, attendete che Browser TVSDK invii l&#39; `AdobePSDK.MediaPlayerStatusChangeEvent` evento con un `event.status` di `MediaPlayerStatus.PREPARED`.

   Per verificare se lo stato corrente dell&#39;oggetto MediaPlayer è almeno PREPARATO.

   ```
   <readonly> status :AdobePSDK.MediaPlayerStatus
   ```

