---
description: Potete inserire annunci nel contenuto VOD.
seo-description: Potete inserire annunci nel contenuto VOD.
seo-title: Sostituire gli intervalli di tempo con un annuncio
title: Sostituire gli intervalli di tempo con un annuncio
uuid: 8f09560c-bca3-4662-bc58-6c9cd0892476
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---


# Sostituire gli intervalli di tempo con un annuncio {#replace-time-ranges-with-an-ad}

Potete inserire annunci nel contenuto VOD.

Le `TimeRanges` tra `begin` e `end` in `localTime` vengono rimosse dalla timeline. Questi intervalli vengono sostituiti da `AdBreak` di `begin` in `begin+replaceDuration`. Se `replacement-duration` non esiste come parametro, il server determina la `Adbreak` restituita.

>[!TIP]
>
>È sempre necessario specificare un `replacement-duration` per gli intervalli personalizzati. Se non è previsto alcun annuncio che sostituisca questo intervallo personalizzato, fornire un `replacement-duration` di 0.

1. Per sostituire gli intervalli con annunci pubblicitari Primetime:

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
                   "type": "replace",
                   "time-range-list": [
                       {
                           "begin": 0,
                           "end": 15000,
                           "replacement-duration": 15000
                       },
                       {
                                "begin": 69000,
                                "end": 99000,
                                "replacement-duration": 30000
                       },
                       {
                           "begin": 251000,
                           "end": 281000,
                           "replacement-duration": 30000
                       },
                       {
                           "begin": 514000,
                           "end": 544000,
                           "replacement-duration": 30000
                       }
                   ]
               },
               "ad": {
                   "targeting": [
                       {
                           "value": "MulAdsAvail12346",
                           "key": "osmfKeyMulAdsAvail12346"
                       }
                   ],
               "domain": "sandbox2.auditude.com",
               "mediaid": "psdk_000105",
               "zoneid": "121781"
               }     
           }
       },   
       "title": "VOD - Replace TimeRange with Auditude Ads",
       "thumbnail": {
           "large": "https://example.com",
           "small": "https://example.com"
       },
       "type": "vod",
       "id": "vod_003"
   }
   ```

