---
description: È possibile designare intervalli di tempo nel contenuto VOD come interruzioni pubblicitarie.
title: Segna intervalli
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '81'
ht-degree: 0%

---


# Segna intervalli {#mark-ranges}

È possibile designare intervalli di tempo nel contenuto VOD come interruzioni pubblicitarie.

Il `TimeRanges` tra `begin` e `end` in `localTime` verrà contrassegnato come `AdBreak` nella timeline. Le altre impostazioni degli annunci vengono ignorate.

>[!TIP]
>
>Se desideri contrassegnare solo alcuni intervalli nel contenuto come annunci, senza inserimento di annunci dinamici, crea un&#39;istanza `CustomRangeMetadata` e specifica il tipo come operazione `MARK` con gli intervalli personalizzati definiti.

1. Tp contrassegna gli intervalli:

   ```
   {   
       "properties": [],
       "stream": {
           "manifests": [
               {
                   "url": "https://d398890tia84ty.cloudfront.net/e2e-vod/cloudfront_vod_hls_tos_30fps.m3u8",
                   "type": "hls"
               }
           ],
   
       "metadata": {
           "time-ranges": {
                   "type": "mark",
               "adjust-seek-position" : true,   
                   "time-range-list": [
                     {
                        "begin": 0,
                        "end": 15000
                       },
                     {
                        "begin": 69000,
                        "end": 99000
                       },
                     {
                         "begin": 251000,
                         "end": 281000
                       },
                     {
                         "begin": 514000,
                         "end": 544000
                       }
                    ]
   
                 }
            }           
       },   
       "title": "VOD - MARK TimeRanges and no ads",
       "thumbnail": {
           "large": "https://example.com",
           "small": "https://example.com"
          },
       "type": "vod",
       "id": "vod_004"
   }
   ```

