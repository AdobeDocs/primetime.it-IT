---
description: È possibile inserire annunci nel contenuto VOD.
title: Sostituire gli intervalli di tempo con un annuncio
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 0%

---


# Sostituisci intervalli di tempo con un annuncio{#replace-time-ranges-with-an-ad}

È possibile inserire annunci nel contenuto VOD.

In questo caso, `TimeRanges` tra `begin` e `end` in `localTime` vengono rimossi dalla timeline. Sono sostituiti da `AdBreak` di `begin` in `begin+replaceDuration`. Se la durata di sostituzione non esiste come parametro, il server determina l&#39;indirizzo di sostituzione restituito.

>[!NOTE]
>
>È sempre necessario fornire una specifica durata di sostituzione per intervalli personalizzati. Se non sono previsti annunci per sostituire questo intervallo personalizzato, fornisci una durata di sostituzione di 0.

Sostituisci gli intervalli con gli annunci ad decision ioning di Primetime.

```
{   
    "properties": [],
    "stream": {
        "manifests": [ {
            "url": 
              "https://d398890tia84ty.cloudfront.net/e2e-vod/cloudfront_vod_hls_tos_30fps.m3u8",
            "type": "hls"
        } ],
                 
        "metadata": {
            "time-ranges": {
                "type": "replace",
                "time-range-list": [ {
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
                } ]
            },
            "ad": {
                "targeting": [ {
                    "value": "MulAdsAvail12346",
                    "key": "osmfKeyMulAdsAvail12346"
                } ],
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

