---
title: Oggetto JSON per interruzioni pubblicitarie dirette
description: Dettagli dell’oggetto JSON quando il valore del tipo è direct ad break
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---


# Oggetto JSON per interruzioni pubblicitarie dirette{#json-object-for-direct-ad-breaks}

Il seguente blocco di codice definisce l&#39;oggetto JSON dei dettagli quando il valore del tipo è direct ad break.

Il `MetadataNode` restituito da `IFeedItemAdapter:getStreamMetadata()` contiene una voce con chiave di tipo `com.adobe.mediacore.metadata.DefaultMetadataKeys.JSON_METADATA_KEY` e un valore di una rappresentazione stringa del valore dell&#39;oggetto JSON dei dettagli qui sotto.

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
| `tag` | Una stringa associata al campo tag in `com.adobe.mediacore.timeline.advertising.AdBreak`. |
| `time` | Indica l&#39;ora di inizio dell&#39;interruzione pubblicitaria, viene mappata sul campo ora in `com.adobe.mediacore.timeline.advertising.AdBreak`. Il valore 0 indica un annuncio pre-roll. |
| `replace` | Indica la durata della sostituzione dell&#39;interruzione pubblicitaria, viene mappata sul campo `replaceDuration` in `com.adobe.mediacore.timeline.advertising.AdBreak`. |
| `ad-list` | Un elenco di annunci da riprodurre durante la data interruzione pubblicitaria, viene mappato sul campo `List<Ad>` in `com.adobe.mediacore.timeline.advertising.AdBreak`. |

Il seguente blocco di codice definisce l&#39;oggetto JSON per l&#39;array di elenchi di annunci.

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
| `url` | L’URL del contenuto dell’annuncio viene mappato sul campo url in `com.adobe.mediacore.timeline.advertising.Ad`. |
| `duration` | La durata dell’annuncio viene mappata sul campo della durata in `com.adobe.mediacore.timeline.advertising.Ad`. |
| `tag` | Una stringa di descrizione. |

