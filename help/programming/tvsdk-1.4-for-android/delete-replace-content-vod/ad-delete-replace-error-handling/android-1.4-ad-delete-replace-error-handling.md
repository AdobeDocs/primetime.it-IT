---
description: TVSDK gestisce gli errori di intervallo di tempo in base al problema specifico, unendo o riordinando gli intervalli di tempo definiti in modo errato.
title: Gestione degli errori di eliminazione e sostituzione degli annunci
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---

# Gestione degli errori di eliminazione e sostituzione degli annunci{#ad-deletion-and-replacement-error-handling}

TVSDK gestisce gli errori di intervallo di tempo in base al problema specifico, unendo o riordinando gli intervalli di tempo definiti in modo errato.

TVSDK tratta con `timeRanges` commettendo errori di unione e riordinamento predefiniti. Innanzitutto, ordina gli intervalli di tempo definiti dal cliente in base al *inizio* tempo. In base a questo ordinamento, unisce quindi intervalli adiacenti e li unisce se sono presenti sottoinsiemi e intersezioni tra gli intervalli.

TVSDK gestisce gli errori dell’intervallo di tempo come segue:

* Fuori servizio: TVSDK riordina gli intervalli di tempo.
* Sottoinsieme: TVSDK unisce i sottoinsiemi dell’intervallo di tempo.
* Intersezione: TVSDK unisce gli intervalli di tempo intersecanti.
* Conflitto per la sostituzione degli intervalli: TVSDK sceglie la durata della sostituzione dal primo elemento visualizzato `timeRange` nel gruppo in conflitto.

TVSDK gestisce i conflitti in modalità di segnalazione con i metadati dell’annuncio come segue:

* Se la modalità di segnalazione dell’annuncio è in conflitto con i metadati dell’intervallo di tempo, questi ultimi hanno sempre la priorità. Ad esempio, se la modalità di segnalazione dell’annuncio è impostata come mappa del server o segnali manifesti e i metadati dell’annuncio contengono anche degli intervalli di tempo MARK, il risultato è che gli intervalli vengono contrassegnati e non vengono inseriti annunci.
* Per gli intervalli REPLACE, se la modalità di segnalazione è impostata come mappa del server o segnali manifest, gli intervalli vengono sostituiti come specificato negli intervalli REPLACE e non vi è inserimento di annunci tramite mappa del server o segnali manifest. Consulta [Modalità di segnalazione dell’annuncio](../../../tvsdk-1.4-for-android/ad-insertion/ad-insertion-metadata/android-1.4-ad-signaling-mode.md).

Se il server non restituisce un valore valido `AdBreaks`:

* TVSDK genera ed elabora un `NOPTimelineOperation` per il vuoto `AdBreak`. Nessun annuncio riprodotto.

Per gli intervalli di tempo con flussi live:

* Sebbene questa funzione di eliminazione/sostituzione di annunci C3 sia progettata per essere supportata solo per VOD, gli intervalli di tempo vengono elaborati anche per i flussi live, se specificato nei metadati dell’annuncio.

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
