---
description: Potrebbe essere necessario sapere se il contenuto multimediale è live o VOD.
seo-description: Potrebbe essere necessario sapere se il contenuto multimediale è live o VOD.
seo-title: Identificare se il contenuto è live o VOD
title: Identificare se il contenuto è live o VOD
uuid: 5455801e-b5eb-4829-bde6-ef4440cd69c5
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Identificare se il contenuto è live o VOD{#identify-whether-the-content-is-live-or-vod}

Potrebbe essere necessario sapere se il contenuto multimediale è live o VOD.

1. Attendete che il browser TVSDK attivi un `AdobePSDK.PSDKEventType.STATUS_CHANGED` evento con un `event.status` di `AdobePSDK.MediaPlayerStatus.PREPARED`.

   Questo passaggio assicura che la risorsa multimediale sia stata caricata correttamente.

   >[!IMPORTANT]
   >
   >Se il browser TVSDK non è almeno nello `PREPARED` stato, il tentativo di chiamare i seguenti metodi genera un `IllegalStateException`.

1. Leggi `live` dall&#39; `MediaPlayerItem` interfaccia:

   ```js
   player.currentItem.live
   ```

