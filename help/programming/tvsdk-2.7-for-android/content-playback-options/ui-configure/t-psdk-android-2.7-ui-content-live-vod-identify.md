---
description: Potrebbe essere necessario sapere se il contenuto multimediale è live o video su richiesta (VOD).
seo-description: Potrebbe essere necessario sapere se il contenuto multimediale è live o video su richiesta (VOD).
seo-title: Identificare se il contenuto è live o VOD
title: Identificare se il contenuto è live o VOD
uuid: d49315ee-8cec-4b79-adbd-a49c2a527424
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Identificare se il contenuto è live o VOD {#identify-whether-the-content-is-live-or-vod}

Potrebbe essere necessario sapere se il contenuto multimediale è live o video su richiesta (VOD).

1. Assicurarsi che il lettore sia almeno nello `PREPARED` stato.
1. Determinare se il `MediaPlayerItem` contenuto è live ( `true`) o VOD ( `false`).

   ```java
   boolean isLive();
   ```
