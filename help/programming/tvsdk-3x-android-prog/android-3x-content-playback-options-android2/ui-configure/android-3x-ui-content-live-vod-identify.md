---
description: Potrebbe essere necessario sapere se il contenuto multimediale è in diretta o video on-demand (VOD).
title: Identifica se il contenuto è live o VOD
exl-id: a75332d9-a23a-423c-8d1f-81b40ca73b21
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
