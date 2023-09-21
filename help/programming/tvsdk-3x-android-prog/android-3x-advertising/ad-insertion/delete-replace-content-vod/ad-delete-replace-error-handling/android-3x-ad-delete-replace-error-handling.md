---
description: TVSDK gestisce gli errori di intervallo di tempo in base al problema specifico unendo o riordinando gli intervalli di tempo definiti in modo errato.
title: Gestione degli errori di eliminazione e sostituzione degli annunci
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# Gestione degli errori di eliminazione e sostituzione degli annunci  {#ad-deletion-and-replacement-error-handling}

TVSDK gestisce gli errori di intervallo di tempo in base al problema specifico unendo o riordinando gli intervalli di tempo definiti in modo errato.

TVSDK gestisce `timeRanges` errori durante i processi di unione e riordinamento predefiniti. Innanzitutto, il lettore ordina gli intervalli di tempo definiti dal cliente in base al *inizio* tempo. In base a questo ordine di ordinamento, se esistono sottoinsiemi e intersezioni tra gli intervalli, TVSDK unisce gli intervalli adiacenti e li unisce.

TVSDK gestisce gli errori di intervallo di tempo con le seguenti opzioni:

* **Fuori servizio** TVSDK riordina gli intervalli di tempo.

* **Sottoinsieme** TVSDK unisce i sottoinsiemi dell’intervallo di tempo.

* **Interseca** TVSDK unisce gli intervalli di tempo intersecanti.

* **Conflitto di sostituisci intervalli** TVSDK seleziona la durata di sostituzione dal primo `timeRange` nel gruppo in conflitto.

TVSDK gestisce i conflitti in modalità di segnalazione con i metadati degli annunci nei seguenti modi:

* Se la modalità di segnalazione dell’annuncio è in conflitto con i metadati dell’intervallo di tempo, questi ultimi hanno sempre la priorità.

  Ad esempio, se la modalità di segnalazione dell’annuncio è impostata come mappa del server o segnali manifesti e nei metadati dell’annuncio sono presenti anche intervalli di tempo MARK, il comportamento risultante è che gli intervalli vengono contrassegnati e non vengono inseriti annunci.
* Per gli intervalli REPLACE, se la modalità di segnalazione è impostata come mappa del server o segnali manifest, gli intervalli vengono sostituiti come specificato negli intervalli REPLACE e non vi è inserimento di annunci tramite mappa del server o segnali manifest.

  Per ulteriori informazioni, vedere *Comportamenti combinati modalità di segnalazione/metadati* tabella in [Effetto sull’inserimento e l’eliminazione di annunci dalla modalità di segnalazione degli annunci](../../../../../tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/delete-replace-content-vod/android-3x-signaling-mode-android.md).

Tenere presente quanto segue:

* Se il server non restituisce un valore valido `AdBreaks`, TVSDK genera ed elabora un `NOPTimelineOperation` per l’AdBreak vuoto, e non viene riprodotto alcun annuncio.

* Anche se l’eliminazione/sostituzione di annunci C3 è progettata per essere supportata solo per VOD, se specificata nei metadati dell’annuncio, gli intervalli di tempo vengono elaborati anche per i flussi live.
