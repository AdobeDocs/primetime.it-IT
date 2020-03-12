---
description: Potete inserire annunci nel contenuto VOD.
seo-description: Potete inserire annunci nel contenuto VOD.
seo-title: Sostituire gli intervalli di tempo con un annuncio
title: Sostituire gli intervalli di tempo con un annuncio
uuid: 50cdcc06-7df5-414b-95d4-c684bc68dce3
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Sostituire gli intervalli di tempo con un annuncio{#replace-time-ranges-with-an-ad}

Potete inserire annunci nel contenuto VOD.

In questo caso, `TimeRanges` tra `begin` e `end` in `localTime` vengono rimossi dalla timeline. Sono sostituiti da un `AdBreak` di `begin` a `begin+replaceDuration`. Se la durata della sostituzione non esiste come parametro, il server determina l&#39;entità dell&#39;interruzione adbreak restituita.

>[!NOTE]
>
>È sempre necessario fornire una specifica durata di sostituzione per gli intervalli personalizzati. Se non sono previsti annunci per sostituire questo intervallo personalizzato, fornire una durata di sostituzione pari a 0.

Sostituisci gli intervalli con annunci pubblicitari con Primetime e con funzioni di decisione.

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

