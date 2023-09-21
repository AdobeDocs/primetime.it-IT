---
title: Oggetto JSON per interruzioni pubblicitarie dirette
description: Fornisce dettagli sull’oggetto JSON quando il valore del tipo è direct ad break
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# Oggetto JSON per interruzioni pubblicitarie dirette{#json-object-for-direct-ad-breaks}

Il blocco di codice seguente definisce l’oggetto JSON dei dettagli quando il valore del tipo è direct ad break.

Il `MetadataNode` restituito da `IFeedItemAdapter:getStreamMetadata()` contiene una voce con chiave di tipo `com.adobe.mediacore.metadata.DefaultMetadataKeys.JSON_METADATA_KEY` e valore di una rappresentazione stringa del valore dell’oggetto JSON dei dettagli riportato di seguito.

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
| `tag` | Una stringa mappata al campo tag in `com.adobe.mediacore.timeline.advertising.AdBreak`. |
| `time` | Indica l’ora di inizio dell’interruzione pubblicitaria, viene mappato sul campo temporale in `com.adobe.mediacore.timeline.advertising.AdBreak`. Il valore 0 indica un annuncio pre-roll. |
| `replace` | Indica la durata della sostituzione dell’interruzione pubblicitaria, viene mappato sulla `replaceDuration` campo in `com.adobe.mediacore.timeline.advertising.AdBreak`. |
| `ad-list` | Un elenco di annunci da riprodurre durante l’interruzione pubblicitaria specificata, mappa su `List<Ad>` campo in `com.adobe.mediacore.timeline.advertising.AdBreak`. |

Il seguente blocco di codice definisce l’oggetto JSON per l’array dell’elenco annunci.

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
| `url` | L’URL del contenuto dell’annuncio, viene mappato sul campo URL in `com.adobe.mediacore.timeline.advertising.Ad`. |
| `duration` | La durata dell’annuncio, corrisponde al campo della durata in `com.adobe.mediacore.timeline.advertising.Ad`. |
| `tag` | Una stringa di descrizione. |
