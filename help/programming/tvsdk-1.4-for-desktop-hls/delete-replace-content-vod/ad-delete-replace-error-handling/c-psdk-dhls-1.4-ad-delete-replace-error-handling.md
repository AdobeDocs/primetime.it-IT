---
description: TVSDK gestisce gli errori dell'intervallo di tempo in base al problema specifico, unendo o riordinando gli intervalli di tempo definiti in modo errato.
seo-description: TVSDK gestisce gli errori dell'intervallo di tempo in base al problema specifico, unendo o riordinando gli intervalli di tempo definiti in modo errato.
seo-title: Gestione degli errori di aggiunta ed eliminazione
title: Gestione degli errori di aggiunta ed eliminazione
uuid: ab153591-0011-44b4-87f9-be0302c2295e
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# Gestione degli errori di aggiunta ed eliminazione {#ad-deletion-and-replacement-error-handling}

TVSDK gestisce gli errori dell&#39;intervallo di tempo in base al problema specifico, unendo o riordinando gli intervalli di tempo definiti in modo errato.

TVSDK gestisce `timeRanges` gli errori eseguendo l&#39;unione e il riordinamento predefiniti. Innanzitutto, ordina gli intervalli di tempo definiti dal cliente in base all&#39;ora di *inizio* . In base a questo ordine di ordinamento, unisce quindi gli intervalli adiacenti e li unisce in presenza di sottoinsiemi e intersezioni tra gli intervalli.

TVSDK gestisce gli errori relativi all’intervallo di tempo come segue:

* Fuori ordine: TVSDK riordina gli intervalli di tempo.
* Subset - TVSDK unisce i sottoinsiemi dell’intervallo di tempo.
* Intersect - TVSDK unisce gli intervalli di tempo intersecanti.
* Sostituire gli intervalli in conflitto - TVSDK sceglie la durata di sostituzione dalla prima visualizzazione `timeRange` nel gruppo in conflitto.

TVSDK gestisce i conflitti in modalità di segnalazione come segue:

* Se gli intervalli REPLACE sono definiti, TVSDK modifica automaticamente la modalità di segnalazione in CUSTOM_RANGE.
* Se gli intervalli DELETE o MARK sono definiti e la modalità di segnalazione è CUSTOM_RANGE, TVSDK elimina o contrassegna questi intervalli. Nessun inserimento di annunci in questo caso.
* Se un intervallo DELETE o MARK definisce una durata di sostituzione, TVSDK ignora questa durata.

Quando il server non restituisce valori validi `AdBreaks`:

* TVSDK genera ed elabora un `NOPTimelineOperation` nome per il vuoto `AdBreak`. Nessuna pubblicità gioca.

## Esempi di errori nell&#39;intervallo di tempo {#time-range-error-examples}

TVSDK risponde a specifiche errate dell&#39;intervallo di tempo unendo o sostituendo gli intervalli di tempo come appropriato.

Nell&#39;esempio seguente sono definiti quattro intervalli di tempo DELETE intersecanti. TVSDK unisce i quattro intervalli di tempo in uno, in modo che l&#39;intervallo di eliminazione effettivo sia compreso tra 0 e 50.

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

Nell&#39;esempio seguente, quattro intervalli di tempo REPLACE sono definiti con intervalli di tempo in conflitto. In questo caso, TVSDK sostituisce 0-50 con 25 annunci. Viene usata la prima durata di sostituzione nell&#39;ordinamento, in quanto vi sono conflitti negli intervalli successivi.

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
