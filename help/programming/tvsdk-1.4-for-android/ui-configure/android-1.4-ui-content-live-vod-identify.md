---
description: In alcuni casi, è necessario sapere se il contenuto multimediale è live o VOD.
seo-description: In alcuni casi, è necessario sapere se il contenuto multimediale è live o VOD.
seo-title: Identificare se il contenuto è live o VOD
title: Identificare se il contenuto è live o VOD
uuid: cd71b8d3-259a-48f8-a6ad-02b57da146a7
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Identificare se il contenuto è live o VOD{#identify-whether-the-content-is-live-or-vod}

In alcuni casi, è necessario sapere se il contenuto multimediale è live o VOD.

1. Assicurarsi che il lettore sia almeno nello stato PREPARATO.
1. Determinate se il `MediaPlayerItem` contenuto è live (true) o VOD (false).

   ```java
   boolean isLive();
   ```

