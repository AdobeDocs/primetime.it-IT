---
description: Alcuni annunci (o creativi) di terze parti non possono essere inseriti nello streaming di contenuti HTTP Live Streaming (HLS)/Dynamic Adaptive Streaming su HTTP (DASH) perché il loro formato video è incompatibile con HLS/DASH. L'inserimento di annunci Adobe Primetime e il browser TVSDK possono tentare facoltativamente di ricompattare (transcodificare) video incompatibili in video m3u8/mpd compatibili.
title: Repackage (transcode) annunci incompatibili
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---


# Ricompila (transcodifica) annunci incompatibili{#repackage-transcode-incompatible-ads}

Alcuni annunci (o creativi) di terze parti non possono essere inseriti nello streaming di contenuti HTTP Live Streaming (HLS)/Dynamic Adaptive Streaming su HTTP (DASH) perché il loro formato video è incompatibile con HLS/DASH. L&#39;inserimento di annunci Adobe Primetime e il browser TVSDK possono tentare facoltativamente di ricompattare (transcodificare) video incompatibili in video m3u8/mpd compatibili.

Gli annunci forniti da varie terze parti, come un agenzia ad server, il tuo partner di inventario o una rete pubblicitaria, vengono spesso consegnati in formati incompatibili, come ad esempio il progressivo download MP4.
