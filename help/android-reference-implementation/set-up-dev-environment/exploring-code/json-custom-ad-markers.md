---
title: Oggetto JSON per marcatori di annunci personalizzati
description: Oggetto JSON per marcatori di annunci personalizzati
copied-description: true
exl-id: 85bcf306-703c-4a0d-b125-df9316fadf69
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---

# Oggetto JSON per marcatori di annunci personalizzati {#json-object-for-custom-ad-markers}

Il blocco di codice seguente definisce l’oggetto JSON &quot;details&quot; (dettagli) quando il tipo è un indicatore di annuncio personalizzato.

Il MetadataNode restituito da IFeedItemAdapter:getStreamMetadata() contiene 2 voci:
1. una voce con chiave di tipo `com.adobe.mediacore.metadata.DefaultMetadataKeys.CUSTOM_AD_MARKERS_METADATA_KEY` e il valore di un&#39;istanza del MetadataNode restituito da `TimeRangeCollection.toMetadata()`.
1. La seconda voce ha una chiave di tipo `com.adobe.mediacore.metadata.DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED` con il valore del *adjust-seek-position* di seguito.

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
| adjust-seek-position | true o false, utilizzato per impostare il valore della chiave com.adobe.mediacore.metadata.DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED in MetadataNode. |
| intervalli di tempo | Matrice di oggetti JSON che indica l’intervallo di tempo per ogni marcatore di annuncio. Ogni voce Oggetto JSON viene mappata su un&#39;istanza di com.adobe.mediacore.utils.TimeRange. |
| time-ranges.begin | Valore in ms che indica l’ora di inizio del marcatore dell’annuncio. |
| time-ranges.end | Valore in ms che indica l’ora di fine del marcatore dell’annuncio. |

Per ulteriori informazioni sul funzionamento dei marcatori degli annunci personalizzati, consulta la documentazione di TVSDK.
