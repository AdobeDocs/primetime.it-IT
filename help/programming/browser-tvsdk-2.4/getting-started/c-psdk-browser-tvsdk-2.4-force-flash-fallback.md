---
description: Il flag forceflash nell’elenco di origine forza il fallback del Flash per un URL. Per questo URL, puoi utilizzare Adobe Flash Player per riprodurre il contenuto.
title: Forzare il fallback del Flash utilizzando l’elenco di origini dei contenuti multimediali
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 0%

---

# Forzare il fallback del Flash utilizzando l’elenco di origini dei contenuti multimediali{#forcing-the-flash-fallback-using-the-media-source-list}

Il flag forceflash nell’elenco di origine forza il fallback del Flash per un URL. Per questo URL, puoi utilizzare Adobe Flash Player per riprodurre il contenuto.

Nell’elenco delle origini dei file multimediali (ad esempio nel `sources.js` file), è possibile impostare `forceflash` a `true`. Ad esempio:

```js
{ 
        "title":"Title of the item listed in the media source list",
        "description":"Description of the item listed in the media source list",
        "isLive":true,
        "content":[ 
            { 
                "format":"HLS",
                "url":"https://path_to_HLS_stream.m3u8"
            },
 
        ],
        "forceflash" : true
},
```
