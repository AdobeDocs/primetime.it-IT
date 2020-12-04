---
description: Potete specificare intervalli di tempo nel contenuto VOD come interruzioni di annuncio.
seo-description: Potete specificare intervalli di tempo nel contenuto VOD come interruzioni di annuncio.
seo-title: Segna intervalli
title: Segna intervalli
uuid: 6ae2adee-fb7a-4cef-a8e8-ecf671ed3660
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 0%

---


# Intervalli di caratteri {#mark-ranges}

Potete specificare intervalli di tempo nel contenuto VOD come interruzioni di annuncio.

La `TimeRanges` tra `begin` e `end` in `localTime` verrà contrassegnata come `AdBreak` nella timeline. Le altre impostazioni degli annunci vengono ignorate.

>[!TIP]
>
>Se desiderate contrassegnare solo alcuni intervalli nel contenuto come annunci, senza inserimento dinamico di annunci, create un&#39;istanza `CustomRangeMetadata` e specificate il tipo come operazione `MARK` con gli intervalli personalizzati definiti.

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

