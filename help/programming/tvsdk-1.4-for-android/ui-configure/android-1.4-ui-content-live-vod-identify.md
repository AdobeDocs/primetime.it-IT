---
description: In alcuni casi, è necessario sapere se il contenuto multimediale è live o VOD.
title: Identificare se il contenuto è live o VOD
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '67'
ht-degree: 0%

---


# Identifica se il contenuto è live o VOD{#identify-whether-the-content-is-live-or-vod}

In alcuni casi, è necessario sapere se il contenuto multimediale è live o VOD.

1. Assicurati che il lettore sia almeno nello stato PREPARATO.
1. Determina se il contenuto `MediaPlayerItem` è live (true) o VOD (false).

   ```java
   boolean isLive();
   ```

