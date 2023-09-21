---
description: Potrebbe essere necessario sapere se il contenuto multimediale è in diretta o video on-demand (VOD).
title: Identifica se il contenuto è live o VOD
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '66'
ht-degree: 0%

---

# Identifica se il contenuto è live o VOD {#identify-whether-the-content-is-live-or-vod}

Potrebbe essere necessario sapere se il contenuto multimediale è in diretta o video on-demand (VOD).

1. Assicurati che il lettore si trovi almeno nel `PREPARED` stato.
1. Determinare se `MediaPlayerItem` il contenuto è live ( `true`) o VOD ( `false`).

   ```java
   boolean isLive();
   ```
