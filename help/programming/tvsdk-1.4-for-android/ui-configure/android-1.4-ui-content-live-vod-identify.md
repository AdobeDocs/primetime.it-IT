---
description: In alcuni casi, è necessario sapere se il contenuto multimediale è in diretta o VOD.
title: Identifica se il contenuto è live o VOD
exl-id: b93cc61b-aa72-4edd-a070-93c111dec339
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '67'
ht-degree: 0%

---

# Identifica se il contenuto è live o VOD{#identify-whether-the-content-is-live-or-vod}

In alcuni casi, è necessario sapere se il contenuto multimediale è in diretta o VOD.

1. Assicurarsi che il lettore sia almeno nello stato PREPARATO.
1. Determinare se `MediaPlayerItem` il contenuto è live (true) o VOD (false).

   ```java
   boolean isLive();
   ```
