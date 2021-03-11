---
title: Casi d'uso speciali
description: Casi d'uso speciali
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 0%

---


# Casi d&#39;uso speciali{#special-use-cases}

TVSDK favorisce le impostazioni dell’intervallo personalizzate rispetto alle impostazioni degli annunci standard. Ad esempio, se gli intervalli MARK sono definiti, le impostazioni di inserimento dell’annuncio vengono ignorate. Se gli intervalli di SOSTITUZIONE sono definiti, TVSDK utilizza automaticamente la modalità di segnalazione `CustomRanges`.

1. `ReplaceRange` senza durata di sostituzione

   Se manca la durata della sostituzione, la durata effettiva della sostituzione è determinata dal server. Anche il numero di annunci inseriti in questo `AdBreak` è determinato dal server.

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

   La durata di sostituzione aggiuntiva viene ignorata.
