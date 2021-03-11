---
title: Sostituisci intervalli di tempo con un annuncio di Adobe Primetime ad decisioning
description: Sostituisci intervalli di tempo con un annuncio di Adobe Primetime ad decisioning
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '52'
ht-degree: 0%

---


# Sostituisci intervalli di tempo con un annuncio pubblicitario di Adobe Primetime {#replace-time-ranges-with-an-adobe-primetime-ad-decisioning-ad}

Rimuovi `TimeRanges` tra `begin` e `end` in `localTime` dalla timeline. Sostituiscilo con un AdBreak di `begin` a `begin+replaceDuration`.

Sostituisci gli intervalli con gli annunci ad decision ioning di Primetime.

```
{   
    "properties": [],
    "stream": {
        "manifests": [ {
            "url": "https://. . ./cloudfront_vod_hls_tos_30fps.m3u8",
            "type": "hls"
        } ],
        "metadata": {
            "time-ranges": {
                "type": "replace",
                "time-range-list": [ {
                    "begin": 0,
                    "end": 15000,
                    "replace-duration": 15000
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

