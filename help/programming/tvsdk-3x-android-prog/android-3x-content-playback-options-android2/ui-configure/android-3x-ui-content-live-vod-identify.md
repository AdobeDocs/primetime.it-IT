---
description: Potrebbe essere necessario sapere se il contenuto multimediale è live o video on demand (VOD).
title: Identificare se il contenuto è live o VOD
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '66'
ht-degree: 0%

---


# Identifica se il contenuto è live o VOD {#identify-whether-the-content-is-live-or-vod}

Potrebbe essere necessario sapere se il contenuto multimediale è live o video on demand (VOD).

1. Assicurati che il lettore sia almeno nello stato `PREPARED`.
1. Determina se il contenuto `MediaPlayerItem` è live ( `true`) o VOD ( `false`).

   ```java
   boolean isLive();
   ```
