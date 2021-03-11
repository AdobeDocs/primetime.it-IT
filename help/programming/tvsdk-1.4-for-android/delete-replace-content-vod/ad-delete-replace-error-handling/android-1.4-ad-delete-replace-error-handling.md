---
description: TVSDK gestisce gli errori dell’intervallo di tempo in base al problema specifico, unendo o riordinando gli intervalli di tempo definiti in modo errato.
title: Eliminazione degli annunci e gestione degli errori di sostituzione
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---


# Eliminazione degli annunci e gestione degli errori di sostituzione{#ad-deletion-and-replacement-error-handling}

TVSDK gestisce gli errori dell’intervallo di tempo in base al problema specifico, unendo o riordinando gli intervalli di tempo definiti in modo errato.

TVSDK gestisce gli errori `timeRanges` effettuando l’unione e il riordino predefiniti. Innanzitutto, ordina gli intervalli di tempo definiti dal cliente in base all&#39; ora *start*. In base a questo ordinamento, unisce quindi gli intervalli adiacenti e li unisce in presenza di sottoinsiemi e intersezioni tra gli intervalli.

TVSDK gestisce gli errori nell’intervallo di tempo come segue:

* Fuori servizio: TVSDK riordina gli intervalli di tempo.
* Sottoinsieme: TVSDK unisce i sottoinsiemi dell’intervallo di tempo.
* Interseziona : TVSDK unisce gli intervalli di tempo intersecanti.
* Conflitto di intervalli di sostituzione : TVSDK sceglie la durata di sostituzione dal primo `timeRange` nel gruppo in conflitto.

TVSDK gestisce i conflitti in modalità di segnalazione con i metadati dell’annuncio come segue:

* Se la modalità di segnalazione degli annunci è in conflitto con i metadati dell&#39;intervallo di tempo, i metadati dell&#39;intervallo di tempo hanno sempre la priorità. Ad esempio, se la modalità di segnalazione degli annunci è impostata come spunti di manifesto o mappa del server e ci sono anche intervalli di tempo MARK nei metadati dell&#39;annuncio, il comportamento risultante è che gli intervalli sono contrassegnati e non vengono inseriti annunci.
* Per gli intervalli di SOSTITUZIONE, se la modalità di segnalazione è impostata come riferimento della mappa del server o del manifesto, gli intervalli vengono sostituiti come specificato negli intervalli di SOSTITUZIONE e non vi è inserimento di annunci tramite la mappa del server o i segnali del manifesto. Consulta [Modalità di segnalazione annunci](../../../tvsdk-1.4-for-android/ad-insertion/ad-insertion-metadata/android-1.4-ad-signaling-mode.md).

Quando il server non restituisce un valore `AdBreaks` valido:

* TVSDK genera ed elabora un `NOPTimelineOperation` per il `AdBreak` vuoto. Nessun annuncio gioca.

Per intervalli di tempo con flussi live:

* Anche se questa funzione di cancellazione/sostituzione degli annunci C3 è destinata a essere supportata solo per i VOD, gli intervalli di tempo vengono elaborati per i flussi live e se specificato nei metadati degli annunci.

## Esempi di errore nell&#39;intervallo di tempo {#time-range-error-examples}

TVSDK risponde alle specifiche errate dell’intervallo di tempo unendo o sostituendo gli intervalli di tempo come appropriato.

Nell’esempio seguente vengono definiti quattro intervalli di tempo DELETE intersecanti. TVSDK unisce i quattro intervalli di tempo in uno, in modo che l’intervallo di eliminazione effettivo sia compreso tra 0 e 50.

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

Nell&#39;esempio seguente, quattro intervalli di tempo SOSTITUISCI sono definiti con intervalli di tempo in conflitto. In questo caso, TVSDK sostituisce 0-50 con 25 annunci. Si abbina alla prima durata di sostituzione nell&#39;ordinamento, perché ci sono conflitti negli intervalli successivi.

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
