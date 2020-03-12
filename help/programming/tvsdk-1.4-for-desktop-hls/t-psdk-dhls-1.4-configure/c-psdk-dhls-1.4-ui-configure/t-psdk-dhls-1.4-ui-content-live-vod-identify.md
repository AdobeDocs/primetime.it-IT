---
description: In alcuni casi, è necessario sapere se il contenuto multimediale è live o VOD.
seo-description: In alcuni casi, è necessario sapere se il contenuto multimediale è live o VOD.
seo-title: Identificare se il contenuto è live o VOD
title: Identificare se il contenuto è live o VOD
uuid: 4d514c46-a1d0-4721-a423-92108126e37e
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Identificare se il contenuto è live o VOD{#identify-whether-the-content-is-live-or-vod}

In alcuni casi, è necessario sapere se il contenuto multimediale è live o VOD.

1. Assicurarsi che il lettore sia almeno nello stato INITIALIZED.
1. Determinate se il `MediaPlayerItem` contenuto è live (true) o VOD (false).

   ```
   function get isLive():Boolean;
   ```

