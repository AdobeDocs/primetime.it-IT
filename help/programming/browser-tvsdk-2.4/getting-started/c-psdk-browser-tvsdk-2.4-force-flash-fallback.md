---
description: Il flag forceflash nell'elenco di origine forza la fallback di Flash per un URL. Per questo URL, puoi utilizzare il Flash Player Adobe per riprodurre il contenuto.
title: Forzare il fallback del Flash utilizzando l'elenco delle sorgenti multimediali
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 2%

---


# Forzare il fallback del Flash utilizzando l&#39;elenco di origine dei file multimediali{#forcing-the-flash-fallback-using-the-media-source-list}

Il flag forceflash nell&#39;elenco di origine forza la fallback di Flash per un URL. Per questo URL, puoi utilizzare il Flash Player Adobe per riprodurre il contenuto.

Nell’elenco delle sorgenti multimediali (ad esempio nel file `sources.js`), puoi impostare `forceflash` su `true`. Ad esempio:

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

