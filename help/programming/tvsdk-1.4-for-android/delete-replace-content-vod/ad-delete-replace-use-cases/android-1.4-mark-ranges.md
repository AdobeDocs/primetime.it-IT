---
description: Potete specificare intervalli di tempo nel contenuto VOD come interruzioni di annuncio.
seo-description: Potete specificare intervalli di tempo nel contenuto VOD come interruzioni di annuncio.
seo-title: Segna intervalli
title: Segna intervalli
uuid: eb99a1c2-6c0c-40a4-bac2-98dce45acfad
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---


# Segna intervalli{#mark-ranges}

Potete specificare intervalli di tempo nel contenuto VOD come interruzioni di annuncio.

In questo caso, `TimeRanges` tra `begin` e `end` in `localTime` verrà contrassegnato come `AdBreak` nella timeline. Le altre impostazioni degli annunci vengono ignorate.

>[!NOTE]
>
>Se desiderate solo contrassegnare alcuni intervalli nel contenuto come annunci (senza inserimento dinamico di annunci), create un&#39;istanza `CustomRangeMetadata` e specificate il tipo come operazione MARK con gli intervalli personalizzati definiti.

1. Segna intervalli.

   ```
   {   
       "properties": [],
       "stream": {
           "manifests": [ {
               "url": "https://d398890tia84ty.cloudfront.net/e2e-vod/cloudfront_vod_hls_tos_30fps.m3u8",
               "type": "hls"
           } ],
           "metadata": {
               "time-ranges": {
                   "type": "mark",
                   "adjust-seek-position" : true,   
                   "time-range-list": [ {
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
                    } ]
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

