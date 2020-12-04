---
seo-title: Oggetto JSON per marcatori di annunci personalizzati
title: Oggetto JSON per marcatori di annunci personalizzati
uuid: 2c05d9ce-a22f-4829-bfea-9dcf0dc7cd6d
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---


# Oggetto JSON per marcatori annunci personalizzati {#json-object-for-custom-ad-markers}

Il blocco di codice riportato di seguito definisce l&#39;oggetto JSON &quot;details&quot; quando il tipo è un indicatore di annunci personalizzato.

Il MetadataNode restituito da IFeedItemAdapter:getStreamMetadata() contiene 2 voci:
1. una voce con chiave di tipo `com.adobe.mediacore.metadata.DefaultMetadataKeys.CUSTOM_AD_MARKERS_METADATA_KEY` e valore di un&#39;istanza di MetadataNode restituita da `TimeRangeCollection.toMetadata()`.
1. La seconda voce ha una chiave di tipo `com.adobe.mediacore.metadata.DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED` con il valore dell&#39;attributo *adjust-search-position* riportato di seguito.

```
“metadata”: {
    “ad” :  {
        “type”: “custom ad markers”,
        “details”: {
            "adjust-seek-position": true,
            "time-ranges": [
                {
                    "begin": 5000,
                    "end":15000
                },
                {
                    "begin": 120000,
                    "end":135000
                }
            ]
        }
    }
}
```

| Proprietà | Descrizione |
|---|---|
| posizione di regolazione | true o false, utilizzato per impostare il valore della chiave com.adobe.mediacore.metadata.DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED nel nodo MetadataNode. |
| intervalli di tempo | Un array di oggetti JSON che indica l&#39;intervallo di tempo per ciascun marcatore annuncio. Ogni voce dell&#39;oggetto JSON viene mappata su un&#39;istanza di com.adobe.mediacore.utils.TimeRange. |
| time-ranges.begin | Valore in ms che indica l&#39;ora di inizio dell&#39;indicatore dell&#39;annuncio. |
| time-ranges.end | Valore in ms che indica l&#39;ora di fine dell&#39;indicatore dell&#39;annuncio. |

Per ulteriori informazioni sul funzionamento dei marcatori pubblicitari personalizzati, consulta la documentazione TVSDK.
