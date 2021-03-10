---
title: Oggetto JSON per marcatori di annunci personalizzati
description: Oggetto JSON per marcatori di annunci personalizzati
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---


# Oggetto JSON per marcatori di annunci personalizzati {#json-object-for-custom-ad-markers}

Il blocco di codice seguente definisce l’oggetto JSON &quot;details&quot; quando il tipo è un marcatore di annunci personalizzato.

Il MetadataNode restituito da IFeedItemAdapter:getStreamMetadata() contiene 2 voci:
1. una voce con chiave di tipo `com.adobe.mediacore.metadata.DefaultMetadataKeys.CUSTOM_AD_MARKERS_METADATA_KEY` e valore di un&#39;istanza del MetadataNode restituito da `TimeRangeCollection.toMetadata()`.
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
| posizione di regolazione-ricerca | true o false, utilizzato per impostare il valore della chiave com.adobe.mediacore.metadata.DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED nel MetadataNode. |
| intervalli di tempo | Matrice di oggetti JSON che indica l’intervallo di tempo per ciascun indicatore pubblicitario. Ogni voce di oggetto JSON viene mappata su un&#39;istanza di com.adobe.mediacore.utils.TimeRange. |
| time-ranges.begin | Valore in ms che indica l&#39;ora di inizio dell&#39;indicatore pubblicitario. |
| time-ranges.end | Valore in ms che indica l&#39;ora di fine dell&#39;indicatore pubblicitario. |

Per ulteriori informazioni sul funzionamento dei marcatori di annunci personalizzati, consulta la documentazione TVSDK .
