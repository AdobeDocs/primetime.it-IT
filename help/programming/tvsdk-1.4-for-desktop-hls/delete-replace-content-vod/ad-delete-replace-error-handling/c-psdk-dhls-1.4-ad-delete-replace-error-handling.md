---
description: TVSDK gestisce gli errori di intervallo di tempo in base al problema specifico, unendo o riordinando gli intervalli di tempo definiti in modo errato.
title: Gestione degli errori di eliminazione e sostituzione degli annunci
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---

# Gestione degli errori di eliminazione e sostituzione degli annunci {#ad-deletion-and-replacement-error-handling}

TVSDK gestisce gli errori di intervallo di tempo in base al problema specifico, unendo o riordinando gli intervalli di tempo definiti in modo errato.

TVSDK tratta con `timeRanges` commettendo errori di unione e riordinamento predefiniti. Innanzitutto, ordina gli intervalli di tempo definiti dal cliente in base al *inizio* tempo. In base a questo ordinamento, unisce quindi intervalli adiacenti e li unisce se sono presenti sottoinsiemi e intersezioni tra gli intervalli.

TVSDK gestisce gli errori dell’intervallo di tempo come segue:

* Fuori servizio: TVSDK riordina gli intervalli di tempo.
* Sottoinsieme: TVSDK unisce i sottoinsiemi dell’intervallo di tempo.
* Intersezione: TVSDK unisce gli intervalli di tempo intersecanti.
* Conflitto per la sostituzione degli intervalli: TVSDK sceglie la durata della sostituzione dal primo elemento visualizzato `timeRange` nel gruppo in conflitto.

TVSDK gestisce i conflitti in modalità di segnalazione come segue:

* Se vengono definiti intervalli REPLACE, TVSDK modifica automaticamente la modalità di segnalazione in CUSTOM_RANGE.
* Se sono definiti intervalli DELETE o intervalli MARK e la modalità di segnalazione è CUSTOM_RANGE, TVSDK elimina o contrassegna tali intervalli. In questo caso non viene inserito alcun annuncio.
* Se un intervallo DELETE o un intervallo MARK definisce una durata di sostituzione, TVSDK ignora tale durata.

Se il server non restituisce un valore valido `AdBreaks`:

* TVSDK genera ed elabora un `NOPTimelineOperation` per il vuoto `AdBreak`. Nessun annuncio riprodotto.

## Esempi di errori nell’intervallo di tempo {#time-range-error-examples}

TVSDK risponde a specifiche di intervalli di tempo errate unendo o sostituendo gli intervalli di tempo in base alle esigenze.

Nell&#39;esempio seguente vengono definiti quattro intervalli di tempo DELETE intersecanti. TVSDK unisce i quattro intervalli di tempo in uno, in modo che l’intervallo di eliminazione effettivo sia compreso tra 0 e 50 secondi.

```
"time-ranges": {
    "type": "delete",
    "time-range-list": [ {
        "begin": 10000,
        "end": 35000
    }, {
        "begin": 20000,
        "end": 50000
    }, {
        "begin": 0,
        "end": 30000
    }, {
        "begin": 30000,
        "end": 40000
    } ]
}
```

Nell&#39;esempio seguente vengono definiti quattro intervalli di tempo REPLACE con intervalli di tempo in conflitto. In questo caso, TVSDK sostituisce 0-50 con 25 annunci. Viene associata alla prima durata di sostituzione nell&#39;ordinamento, in quanto sono presenti conflitti negli intervalli successivi.

```
"time-ranges": {
    "type": "replace",
    "time-range-list": [ {
        "begin": 10000,
        "end": 35000,
        "replace-duration": 15000
    }, {
        "begin": 20000,
        "end": 50000,
        "replace-duration": 20000
    }, {
        "begin": 0,
        "end": 30000,
        "replace-duration": 25000
    }, {
        "begin": 30000,
        "end": 40000,
        "replace-duration": 30000
    } ]
}
```
