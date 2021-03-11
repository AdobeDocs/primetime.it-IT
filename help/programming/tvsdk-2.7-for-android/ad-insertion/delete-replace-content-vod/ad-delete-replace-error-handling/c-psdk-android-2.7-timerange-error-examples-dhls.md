---
description: TVSDK risponde alle specifiche errate dell’intervallo di tempo unendo o sostituendo gli intervalli di tempo come appropriato.
title: Esempi di errori nell’intervallo di tempo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---


# Esempi di errore nell&#39;intervallo di tempo{#time-range-error-examples}

TVSDK risponde alle specifiche errate dell’intervallo di tempo unendo o sostituendo gli intervalli di tempo come appropriato.

**Intervallo di tempo DELETE**

Nell’esempio seguente vengono definiti quattro intervalli di tempo DELETE intersecanti. TVSDK unisce i quattro intervalli di tempo in uno, in modo che l’intervallo di eliminazione effettivo sia compreso tra 0 e 50.

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

Nell&#39;esempio seguente, quattro intervalli di tempo SOSTITUISCI sono definiti con intervalli di tempo in conflitto. In questo caso, TVSDK sostituisce 0-50 con 25 annunci. Si abbina alla prima durata di sostituzione nell&#39;ordinamento, perché ci sono conflitti negli intervalli successivi.

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

