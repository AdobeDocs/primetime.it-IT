---
title: Casi d’uso speciali
description: Casi d’uso speciali
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 0%

---

# Casi d’uso speciali{#special-use-cases}

TVSDK favorisce le impostazioni di intervallo personalizzate rispetto alle impostazioni di annuncio standard. Ad esempio, se sono definiti intervalli MARK, le impostazioni di inserimento dell’annuncio vengono ignorate. Se si definiscono gli intervalli REPLACE, TVSDK utilizza automaticamente `CustomRanges` modalità di segnalazione.

1. `ReplaceRange` senza durata di sostituzione

   Se la durata della sostituzione non è presente, la durata effettiva della sostituzione viene determinata dal server. Il numero di annunci inseriti in questo `AdBreak` è determinato anche dal server.

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
