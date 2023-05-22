---
title: Oggetto JSON per annunci Primetime
description: Il blocco di codice seguente definisce i dettagli dell’oggetto JSON quando il valore del tipo è Annunci Primetime.
exl-id: b1392781-2dfb-4934-b1ce-1c761cbfb22d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---

# Oggetto JSON per annunci Primetime {#json-object-for-primetime-ads}

Il blocco di codice seguente definisce i dettagli dell’oggetto JSON quando il valore del tipo è Annunci Primetime.

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
| dominio | Dominio annunci Primetime da utilizzare per le richieste di annunci. |
| mediaid | Il mediaid che è stato impostato negli annunci Primetime per questo contenuto. |
| zoneid | Il Primetime annunci zoneid. Per ulteriori informazioni, consulta la documentazione sugli annunci di Primetime. |
| targeting | Array di coppie chiave/valore utilizzate per il targeting di annunci specifici per il contenuto. |

Consulta [com.adobe.mediacore.metadata.AuditudeSettings](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/metadata/AuditudeSettings.html) per ulteriori informazioni sul valore di questi attributi.
