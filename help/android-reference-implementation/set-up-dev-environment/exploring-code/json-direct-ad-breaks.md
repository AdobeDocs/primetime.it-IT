---
seo-title: Oggetto JSON per interruzioni pubblicitarie dirette
title: Oggetto JSON per interruzioni pubblicitarie dirette
uuid: ffb901f4-0a8b-40fe-b6ba-5ffebc324cf2
description: Specifica l'oggetto JSON quando il valore del tipo è direct ad break
seo-description: Specifica l'oggetto JSON quando il valore del tipo è direct ad break
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 0%

---


# Oggetto JSON per interruzioni pubblicitarie dirette{#json-object-for-direct-ad-breaks}

Il seguente blocco di codice definisce l&#39;oggetto JSON dei dettagli quando il valore del tipo è direct ad break.

La `MetadataNode` restituita da `IFeedItemAdapter:getStreamMetadata()` contiene una voce con chiave di tipo `com.adobe.mediacore.metadata.DefaultMetadataKeys.JSON_METADATA_KEY` e valore di una rappresentazione in formato stringa del valore dell&#39;oggetto JSON di dettaglio riportato di seguito.

```
“metadata”: { 
    “ad” :  { 
        “type”: “direct ad breaks”, 
        “details”: { 
            "ad-breaks": [ 
                { 
                    "tag": "break-001", 
                    "time": 0, 
                    "replace": 0, 
                    "ad-list": [ 
                        { 
                        }, 
                        { 
                        } 
                    ] 
                }, 
                { 
                    "tag": "break-002", 
                    "time": 300000, 
                    "replace": 0, 
                    "ad-list": [ 
                        { 
                        } 
                    ] 
                } 
            ] 
        } 
    } 
} 
```

| Proprietà | Descrizione |
|---|---|
| `tag` | Una stringa che viene mappata sul campo tag in `com.adobe.mediacore.timeline.advertising.AdBreak`. |
| `time` | Indica l&#39;ora di inizio per l&#39;interruzione dell&#39;annuncio, viene mappata sul campo ora in `com.adobe.mediacore.timeline.advertising.AdBreak`. Il valore 0 indica un annuncio pre-roll. |
| `replace` | Indica la durata della sostituzione dell&#39;interruzione dell&#39;annuncio, viene mappata sul campo `replaceDuration` in `com.adobe.mediacore.timeline.advertising.AdBreak`. |
| `ad-list` | Un elenco di annunci da riprodurre durante l&#39;interruzione dell&#39;annuncio, viene mappato sul campo `List<Ad>` in `com.adobe.mediacore.timeline.advertising.AdBreak`. |

Il seguente blocco di codice definisce l&#39;oggetto JSON per l&#39;array ad elenco.

```
"ad-list": [ 
    { 
        "url": "https://cdn.auditude.com/player/downloads/data/espn/ads/csx/prog_index.m3u8", 
        "duration": 15000, 
        "tag": "1st break - 1st ad" 
    }, 
    { 
        "url": "https://cdn.auditude.com/player/downloads/data/espn/ads/csx/prog_index.m3u8", 
        "duration": 30000, 
        "tag": "1st break - 2nd ad" 
    } 
], 
```

| Proprietà | Descrizione |
|---|---|
| `url` | L&#39;URL del contenuto dell&#39;annuncio viene mappato sul campo url in `com.adobe.mediacore.timeline.advertising.Ad`. |
| `duration` | La durata dell&#39;annuncio viene mappata sul campo durata in `com.adobe.mediacore.timeline.advertising.Ad`. |
| `tag` | Una stringa di descrizione. |

