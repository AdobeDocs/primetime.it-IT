---
title: Oggetto JSON per annunci Primetime
description: Il blocco di codice seguente definisce i dettagli dell'oggetto JSON quando il valore del tipo è Primetime ads.
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---


# Oggetto JSON per annunci Primetime {#json-object-for-primetime-ads}

Il blocco di codice seguente definisce i dettagli dell&#39;oggetto JSON quando il valore del tipo è Primetime ads.

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
| dominio | Dominio degli annunci Primetime da utilizzare per le richieste di annunci. |
| mediana | Il mediaid configurato negli annunci Primetime per questo contenuto. |
| zoneid | Primetime ads zoneid. Per ulteriori informazioni, consulta la documentazione sugli annunci Primetime . |
| targeting | Array di coppie chiave/valore utilizzate per il targeting di annunci specifici per il contenuto. |

Per ulteriori informazioni sul valore di questi attributi, consulta [com.adobe.mediacore.metadata.AuditudeSettings](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/metadata/AuditudeSettings.html) .