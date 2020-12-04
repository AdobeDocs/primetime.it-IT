---
description: 'null'
seo-description: 'null'
seo-title: Casi di utilizzo speciali
title: Casi di utilizzo speciali
uuid: 066bc256-4fdf-4083-b23e-0a916b3b532f
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 0%

---


# Casi di utilizzo speciali{#special-use-cases}

TVSDK privilegia le impostazioni dell&#39;intervallo personalizzate rispetto alle impostazioni dell&#39;annuncio standard. Ad esempio, se gli intervalli MARK sono definiti, le impostazioni di inserimento dell&#39;annuncio vengono ignorate. Se gli intervalli REPLACE sono definiti, TVSDK utilizza automaticamente la modalità di segnalazione `CustomRanges`.

1. `ReplaceRange` senza durata di sostituzione

   Se manca la durata della sostituzione, la durata effettiva della sostituzione è determinata dal server. Il numero di annunci inseriti in questo `AdBreak` è anche determinato dal server.

   ```
   {
       "properties": [],
       "stream": {
           "manifests": [ {
               "url": "https://. . ./vanilla/index.m3u8",
               "type": "hls"
           } ],
           "metadata": {
               "signaling-mode": "custom time ranges",
               "time-ranges": {
                   "type": "replace",
                   "adjust-seek-position": true,
                   "time-range-list": [{
                   "begin": 0,
                   "end": 30000
               }, {
                   "begin": 60000,
                   "end": 75000
               }, {
                   "begin": 255000,
                   "end": 300000
               } ]
               },
               "ad": {             
                   "domain": "sandbox2.auditude.com",
                   "mediaid": "psdk_000105",
                   "zoneid": "121781"
               }     
           }
       },
       "title": "Verify 30Sec Pre-Roll, 15 Sec Mid roll Ad and 
       45 second Post-Roll can be replaced in one shot.",
       "thumbnail": {
           "large": "https://example.com",
           "small": "https://example.com"
       },
       "type": "vod",
       "id": "vod_001"
   }
   ```

1. Intervalli MARK e DELETE con durata di sostituzione

   La durata supplementare della sostituzione viene ignorata.
