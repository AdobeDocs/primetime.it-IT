---
description: Il flag forceflash nell’elenco di origine forza il fallback del Flash per un URL. Per questo URL, puoi utilizzare Adobe Flash Player per riprodurre il contenuto.
title: Forzare il fallback del Flash utilizzando l’elenco di origini dei contenuti multimediali
exl-id: 657bf9b1-d911-489d-80ca-2956b008431b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
