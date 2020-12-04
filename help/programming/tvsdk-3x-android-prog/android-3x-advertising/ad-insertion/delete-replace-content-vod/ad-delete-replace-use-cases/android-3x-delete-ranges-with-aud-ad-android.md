---
description: È possibile rimuovere gli intervalli di tempo tra inizio e fine in localeTime dalla timeline.
seo-description: È possibile rimuovere gli intervalli di tempo tra inizio e fine in localeTime dalla timeline.
seo-title: Elimina intervalli
title: Elimina intervalli
uuid: 2aaea7a0-5d52-49a1-901c-f71e4b081d91
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 0%

---


# Elimina intervalli {#delete-ranges}

È possibile rimuovere `TimeRanges` tra `begin` e `end` in `localTime` dalla timeline.

>[!TIP]
>
>Per rimuovere solo alcuni intervalli dal contenuto, create un&#39;istanza `CustomRangeMetadata` e specificate il tipo come operazione `DELETE` con gli intervalli personalizzati definiti.

La mappa dell&#39;annuncio deve essere utilizzata come definita dal server dell&#39;annuncio.

1. Per eliminare gli intervalli con un annuncio pubblicitario  Adobe Primetime:

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
                   "type": "delete",
                   "time-range-list": [
                       {
                           "begin": 0,
                           "end": 20000
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
       "title": "VOD - DELETE TimeRange with xm-replace_text Phrase Ads",
       "thumbnail": {
           "large": "https://example.com",
           "small": "https://example.com"
       },
       "type": "vod",
       "id": "vod_003"
   },
   ```
