---
description: In alcuni casi, è necessario sapere se il contenuto multimediale è in diretta o VOD.
title: Identifica se il contenuto è live o VOD
exl-id: 180eb515-5bc1-4b32-babf-bcc640ebfa72
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '67'
ht-degree: 0%

---

# Identifica se il contenuto è live o VOD{#identify-whether-the-content-is-live-or-vod}

In alcuni casi, è necessario sapere se il contenuto multimediale è in diretta o VOD.

1. Assicurati che il lettore si trovi almeno nello stato INIZIALIZZATO.
1. Determinare se `MediaPlayerItem` il contenuto è live (true) o VOD (false).

   ```
   function get isLive():Boolean;
   ```
