---
description: Prima di poter utilizzare la maggior parte dei metodi del lettore TVSDK del browser, il lettore deve trovarsi in uno stato valido.
title: Attesa di uno stato valido
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 0%

---

# Attesa di uno stato valido {#wait-for-a-valid-state}

Prima di poter utilizzare la maggior parte dei metodi del lettore TVSDK del browser, il lettore deve trovarsi in uno stato valido.

Il lettore si sposta attraverso vari stati. L’attesa che il lettore si trovi nello stato corretto assicura che la risorsa multimediale sia stata caricata correttamente. Se il lettore non si trova almeno nello stato richiesto, vengono lanciati molti metodi del lettore `IllegalStateException`.

Lo stato richiesto è in genere PREPARATO.

1. Per confermare che lo stato è PREPARATO:

   Quando il lettore viene inizializzato, attendi che il browser TVSDK invii il `AdobePSDK.MediaPlayerStatusChangeEvent` evento con un `event.status` di `MediaPlayerStatus.PREPARED`.

   Per verificare se lo stato corrente dell&#39;oggetto MediaPlayer è almeno READY.

   ```
   <readonly> status :AdobePSDK.MediaPlayerStatus
   ```
