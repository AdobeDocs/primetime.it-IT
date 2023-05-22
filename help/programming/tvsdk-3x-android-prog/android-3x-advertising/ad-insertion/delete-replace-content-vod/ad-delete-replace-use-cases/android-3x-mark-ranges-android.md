---
description: È possibile designare gli intervalli di tempo nel contenuto VOD come interruzioni pubblicitarie.
title: Contrassegna intervalli
exl-id: 904d4d33-6421-44cf-8699-af59a0f7aa58
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '81'
ht-degree: 0%

---

# Contrassegna intervalli {#mark-ranges}

È possibile designare gli intervalli di tempo nel contenuto VOD come interruzioni pubblicitarie.

Il `TimeRanges` tra `begin` e `end` in `localTime` sarà contrassegnato come `AdBreak` nella timeline. Altre impostazioni annuncio vengono ignorate.

>[!TIP]
>
>Se desideri contrassegnare solo determinati intervalli nel contenuto come annunci, senza inserimento di annunci dinamici, crea un `CustomRangeMetadata` e specifica il tipo come `MARK` con gli intervalli personalizzati definiti.

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
