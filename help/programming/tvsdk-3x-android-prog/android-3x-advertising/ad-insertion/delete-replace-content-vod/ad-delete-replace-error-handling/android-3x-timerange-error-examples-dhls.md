---
description: TVSDK risponde a specifiche errate dell'intervallo di tempo unendo o sostituendo gli intervalli di tempo come appropriato.
seo-description: TVSDK risponde a specifiche errate dell'intervallo di tempo unendo o sostituendo gli intervalli di tempo come appropriato.
seo-title: Esempi di errori nell'intervallo di tempo
title: Esempi di errori nell'intervallo di tempo
uuid: 25ac5985-a844-452e-ac95-5006fdf413e6
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 0%

---


# Esempi di errori dell&#39;intervallo di tempo {#time-range-error-examples}

TVSDK risponde a specifiche errate dell&#39;intervallo di tempo unendo o sostituendo gli intervalli di tempo come appropriato.

**Intervallo di tempo DELETE**

Nell&#39;esempio seguente sono definiti quattro intervalli di tempo DELETE intersecanti. TVSDK unisce i quattro intervalli di tempo in uno, in modo che l&#39;intervallo di eliminazione effettivo sia compreso tra 0 e 50.

```
"time-ranges": {
    "type": "delete",
    "time-range-list": [
        {
            "begin": 10000,
            "end": 35000
        },
        {
            "begin": 20000,
            "end": 50000
        },
        {
            "begin": 0,
            "end": 30000
        },
        {
            "begin": 30000,
            "end": 40000
        }
    ]
}
```

**Intervallo di tempo di sostituzione**

Nell&#39;esempio seguente, quattro intervalli di tempo REPLACE sono definiti con intervalli di tempo in conflitto. In questo caso, TVSDK sostituisce 0-50 con 25 annunci. Viene usata la prima durata di sostituzione nell&#39;ordinamento, in quanto vi sono conflitti negli intervalli successivi.

```
"time-ranges": {
    "type": "replace",
    "time-range-list": [
        {
            "begin": 10000,
            "end": 35000,
            "replace-duration": 15000
        },
        {
            "begin": 20000,
            "end": 50000,
            "replace-duration": 20000
        },
        {
            "begin": 0,
            "end": 30000,
            "replace-duration": 25000
        },
        {
            "begin": 30000,
            "end": 40000,
            "replace-duration": 30000
        }
    ]
}
```
