---
description: Potrebbe essere necessario sapere se il contenuto multimediale è live o VOD.
seo-description: Potrebbe essere necessario sapere se il contenuto multimediale è live o VOD.
seo-title: Identificare se il contenuto è live o VOD
title: Identificare se il contenuto è live o VOD
uuid: 5455801e-b5eb-4829-bde6-ef4440cd69c5
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---


# Identificare se il contenuto è live o VOD{#identify-whether-the-content-is-live-or-vod}

Potrebbe essere necessario sapere se il contenuto multimediale è live o VOD.

1. Attendete che il TVSDK del browser attivi un evento `AdobePSDK.PSDKEventType.STATUS_CHANGED` con `event.status` di `AdobePSDK.MediaPlayerStatus.PREPARED`.

   Questo passaggio assicura che la risorsa multimediale sia stata caricata correttamente.

   >[!IMPORTANT]
   >
   >Se TVSDK browser non è almeno nello stato `PREPARED`, il tentativo di chiamare i seguenti metodi genera un `IllegalStateException`.

1. Leggi `live` dall&#39;interfaccia `MediaPlayerItem`:

   ```js
   player.currentItem.live
   ```

