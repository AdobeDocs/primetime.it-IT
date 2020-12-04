---
seo-title: Oggetto JSON per annunci Primetime
title: Oggetto JSON per annunci Primetime
uuid: acf968d2-9856-4ed6-a046-1ac17d176571
description: Il blocco di codice riportato di seguito definisce l'oggetto JSON dei dettagli quando il valore del tipo è Primetime ads.
seo-description: Il blocco di codice riportato di seguito definisce l'oggetto JSON dei dettagli quando il valore del tipo è Primetime ads.
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---


# Oggetto JSON per annunci Primetime {#json-object-for-primetime-ads}

Il blocco di codice riportato di seguito definisce l&#39;oggetto JSON dei dettagli quando il valore del tipo è Primetime ads.

```
“metadata”: {
    “ad” :  {
        “type”: “Primetime ads”,
        “details”: {
            "domain": "sandbox2.auditude.com",
            "mediaid": "rom_asset_case_1",
            "zoneid": "109754",
            "targeting": [
                {
                    "key": "osmfKeyMulAdsAvail12346",
                    "value": "MulAdsAvail12346"
                }
            ]
        }
    }
}
```

| Proprietà | Descrizione |
|---|---|
| domain | Il dominio degli annunci Primetime da utilizzare per le richieste di annunci. |
| mediaid | Il valore mediaid configurato in annunci Primetime per questo contenuto. |
| zoneid | Primetime ads zoneid. Per ulteriori informazioni, consulta la documentazione relativa agli annunci Primetime. |
| targeting | Un array di coppie chiave/valore utilizzate per il targeting di annunci specifici per il contenuto. |

Per ulteriori informazioni sul valore di questi attributi, vedere [com.adobe.mediacore.metadata.AuditudeSettings](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/metadata/AuditudeSettings.html).