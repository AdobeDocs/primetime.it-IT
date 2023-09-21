---
description: TVSDK risponde a specifiche di intervalli di tempo errate unendo o sostituendo gli intervalli di tempo in base alle esigenze.
title: Esempi di errori nell’intervallo di tempo
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---

# Esempi di errori nell’intervallo di tempo {#time-range-error-examples}

TVSDK risponde a specifiche di intervalli di tempo errate unendo o sostituendo gli intervalli di tempo in base alle esigenze.

**Intervallo di tempo DELETE**

Nell&#39;esempio seguente vengono definiti quattro intervalli di tempo DELETE intersecanti. TVSDK unisce i quattro intervalli di tempo in uno, in modo che l’intervallo di eliminazione effettivo sia compreso tra 0 e 50 secondi.

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

**Sostituisci intervallo di tempo**

Nell&#39;esempio seguente vengono definiti quattro intervalli di tempo REPLACE con intervalli di tempo in conflitto. In questo caso, TVSDK sostituisce 0-50 con 25 annunci. Viene associata alla prima durata di sostituzione nell&#39;ordinamento, in quanto sono presenti conflitti negli intervalli successivi.

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
