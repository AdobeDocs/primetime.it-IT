---
description: Potrebbe essere necessario sapere se il contenuto multimediale è live o VOD.
title: Identificare se il contenuto è live o VOD
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '85'
ht-degree: 0%

---


# Identifica se il contenuto è live o VOD{#identify-whether-the-content-is-live-or-vod}

Potrebbe essere necessario sapere se il contenuto multimediale è live o VOD.

1. Attendi che il browser TVSDK attivi un evento `AdobePSDK.PSDKEventType.STATUS_CHANGED` con `event.status` di `AdobePSDK.MediaPlayerStatus.PREPARED`.

   Questo passaggio assicura che la risorsa multimediale sia stata caricata correttamente.

   >[!IMPORTANT]
   >
   >Se il browser TVSDK non è almeno in uno stato `PREPARED`, il tentativo di chiamare i metodi seguenti genera un `IllegalStateException`.

1. Leggi `live` dall&#39;interfaccia `MediaPlayerItem`:

   ```js
   player.currentItem.live
   ```

