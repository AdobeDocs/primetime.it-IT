---
description: Potrebbe essere necessario sapere se il contenuto multimediale è live o video su richiesta (VOD).
seo-description: Potrebbe essere necessario sapere se il contenuto multimediale è live o video su richiesta (VOD).
seo-title: Identificare se il contenuto è live o VOD
title: Identificare se il contenuto è live o VOD
uuid: e6a66104-97fb-438a-8356-e21f94058c85
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Identificare se il contenuto è live o VOD {#identify-whether-the-content-is-live-or-vod}

Potrebbe essere necessario sapere se il contenuto multimediale è live o video su richiesta (VOD).

1. Assicurarsi che il lettore sia almeno nello `PREPARED` stato.
1. Determinare se il `MediaPlayerItem` contenuto è live ( `true`) o VOD ( `false`).

   ```java
   boolean isLive();
   ```
