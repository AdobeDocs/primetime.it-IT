---
description: Il flag forceflash nell'elenco di origine forza il fallback Flash per un URL. Per questo URL, potete utilizzare  Flash Player Adobe per riprodurre il contenuto.
seo-description: Il flag forceflash nell'elenco di origine forza il fallback Flash per un URL. Per questo URL, potete utilizzare  Flash Player Adobe per riprodurre il contenuto.
seo-title: Forzare il fallback del Flash utilizzando l'elenco di origine del file multimediale
title: Forzare il fallback del Flash utilizzando l'elenco di origine del file multimediale
uuid: 04b09734-15f7-4e7e-8802-344f550f9b05
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 1%

---


# Forzare il fallback del Flash utilizzando l&#39;elenco di origine multimediale{#forcing-the-flash-fallback-using-the-media-source-list}

Il flag forceflash nell&#39;elenco di origine forza il fallback Flash per un URL. Per questo URL, potete utilizzare  Flash Player Adobe per riprodurre il contenuto.

Nell&#39;elenco di origine multimediale (ad esempio nel file `sources.js`), è possibile impostare `forceflash` su `true`. Ad esempio:

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

