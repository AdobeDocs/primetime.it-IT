---
description: Alcuni annunci di terze parti (o creativi) non possono essere uniti nel flusso di contenuto HTTP Live Streaming (HLS)/Dynamic Adaptive Streaming over HTTP (DASH) perché il loro formato video è incompatibile con HLS/DASH. Adobe Primetime ad insertion e Browser TVSDK possono opzionalmente tentare di ricompilare (transcodificare) video incompatibili in video m3u8/mpd compatibili.
title: Annunci non compatibili con il riconfezionamento (transcodifica)
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---

# Annunci non compatibili con il riconfezionamento (transcodifica){#repackage-transcode-incompatible-ads}

Alcuni annunci di terze parti (o creativi) non possono essere uniti nel flusso di contenuto HTTP Live Streaming (HLS)/Dynamic Adaptive Streaming over HTTP (DASH) perché il loro formato video è incompatibile con HLS/DASH. Adobe Primetime ad insertion e Browser TVSDK possono opzionalmente tentare di ricompilare (transcodificare) video incompatibili in video m3u8/mpd compatibili.

Gli annunci forniti da terze parti, come ad esempio un server di annunci di un&#39;agenzia, un partner di inventario o una rete di annunci, vengono spesso consegnati in formati incompatibili, come ad esempio MP4 con download progressivo.
