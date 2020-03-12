---
description: Potete inserire annunci nel contenuto VOD.
seo-description: Potete inserire annunci nel contenuto VOD.
seo-title: Sostituire gli intervalli di tempo con un annuncio
title: Sostituire gli intervalli di tempo con un annuncio
uuid: c1d93389-cba4-4db0-877d-dbdc5183683c
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Sostituire gli intervalli di tempo con un annuncio {#replace-time-ranges-with-an-ad}

Potete inserire annunci nel contenuto VOD.

I `TimeRanges` valori compresi tra `begin` e `end` in `localTime` vengono rimossi dalla timeline. Questi intervalli vengono sostituiti da un `AdBreak` valore `begin` a `begin+replaceDuration`. Se `replacement-duration` non esiste come parametro, il server determina la data di restituzione `Adbreak`.

>[!TIP]
>
>È sempre necessario fornire un `replacement-duration` per gli intervalli personalizzati. Se non sono previsti annunci per sostituire l&#39;intervallo personalizzato, immetti `replacement-duration` 0.

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
