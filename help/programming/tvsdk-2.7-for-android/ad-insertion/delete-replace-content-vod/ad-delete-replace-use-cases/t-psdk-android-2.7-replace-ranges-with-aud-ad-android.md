---
description: Puoi inserire annunci nel contenuto VOD.
title: Sostituire gli intervalli di tempo con un annuncio
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 0%

---

# Sostituire gli intervalli di tempo con un annuncio {#replace-time-ranges-with-an-ad}

Puoi inserire annunci nel contenuto VOD.

Il `TimeRanges` tra `begin` e `end` in `localTime` vengono rimossi dalla timeline. Questi intervalli sono sostituiti da un `AdBreak` di `begin` a `begin+replaceDuration`. Se il `replacement-duration` non esiste come parametro, il server effettua la determinazione sul restituito `Adbreak`.

>[!TIP]
>
>Devi sempre fornire un `replacement-duration` per intervalli personalizzati. Se nessun annuncio intende sostituire questo intervallo personalizzato, fornisci un `replacement-duration` di 0.

1. Per sostituire gli intervalli con annunci di Primetime ad decisioningads:

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
