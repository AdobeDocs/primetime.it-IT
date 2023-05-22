---
description: Alcuni annunci di terze parti (o creativi) non possono essere uniti nel flusso di contenuto HTTP Live Streaming (HLS)/Dynamic Adaptive Streaming over HTTP (DASH) perché il loro formato video è incompatibile con HLS/DASH. Adobe Primetime ad insertion e Browser TVSDK possono opzionalmente tentare di ricompilare (transcodificare) video incompatibili in video m3u8/mpd compatibili.
title: Annunci non compatibili con il riconfezionamento (transcodifica)
exl-id: aaa78d5a-4b4b-4d50-b516-d39b47174487
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---

# Annunci non compatibili con il riconfezionamento (transcodifica){#repackage-transcode-incompatible-ads}

Alcuni annunci di terze parti (o creativi) non possono essere uniti nel flusso di contenuto HTTP Live Streaming (HLS)/Dynamic Adaptive Streaming over HTTP (DASH) perché il loro formato video è incompatibile con HLS/DASH. Adobe Primetime ad insertion e Browser TVSDK possono opzionalmente tentare di ricompilare (transcodificare) video incompatibili in video m3u8/mpd compatibili.

Gli annunci forniti da terze parti, come ad esempio un server di annunci di un&#39;agenzia, un partner di inventario o una rete di annunci, vengono spesso consegnati in formati incompatibili, come ad esempio MP4 con download progressivo.
