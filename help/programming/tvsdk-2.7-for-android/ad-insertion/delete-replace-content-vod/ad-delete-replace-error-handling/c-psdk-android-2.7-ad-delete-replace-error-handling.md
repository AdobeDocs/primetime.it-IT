---
description: TVSDK gestisce gli errori dell’intervallo di tempo in base al problema specifico unendo o riordinando gli intervalli di tempo definiti in modo errato.
title: Eliminazione degli annunci e gestione degli errori di sostituzione
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---


# Panoramica {#ad-deletion-and-replacement-error-handling-overview}

TVSDK gestisce gli errori dell’intervallo di tempo in base al problema specifico unendo o riordinando gli intervalli di tempo definiti in modo errato.

TVSDK gestisce gli errori `timeRanges` tramite i processi di unione e riordinamento predefiniti. Innanzitutto, il lettore ordina gli intervalli di tempo definiti dal cliente in base all&#39; ora *start*. In base a questo ordinamento, se ci sono sottoinsiemi e intersezioni tra gli intervalli, TVSDK unisce intervalli adiacenti e unisce questi intervalli.

TVSDK gestisce gli errori nell’intervallo di tempo con le seguenti opzioni:

* **Out of** orderTVSDK riordina gli intervalli di tempo.

* **** SubsetTVSDK unisce i sottoinsiemi dell’intervallo di tempo.

* **** IntersectTVSDK unisce gli intervalli di tempo intersecanti.

* **Sostituisci intervalli** conflittoTVSDK seleziona la durata della sostituzione dalla prima  `timeRange` che viene visualizzata nel gruppo in conflitto.

TVSDK gestisce i conflitti in modalità di segnalazione con i metadati degli annunci nei seguenti modi:

* Se la modalità di segnalazione degli annunci è in conflitto con i metadati dell&#39;intervallo di tempo, i metadati dell&#39;intervallo di tempo hanno sempre la priorità.

   Ad esempio, se la modalità di segnalazione degli annunci è impostata come spunti di manifesto o mappa del server e nei metadati degli annunci sono presenti anche intervalli di tempo MARK, il comportamento risultante è che gli intervalli sono contrassegnati e non vengono inseriti annunci.
* Per gli intervalli REPLACE, se la modalità di segnalazione è impostata come riferimento della mappa del server o del manifesto, gli intervalli vengono sostituiti come specificato negli intervalli REPLACE e non vi è inserimento di annunci tramite la mappa del server o i segnali del manifesto.

   Per ulteriori informazioni, consulta la tabella *Modalità di segnalazione / Comportamenti combinazione metadati* in [Effetti sull’inserimento e sull’eliminazione di annunci dalla modalità di segnalazione di annunci...](../../../../tvsdk-2.7-for-android/ad-insertion/delete-replace-content-vod/c-psdk-android-2.7-signaling-mode-metadata-combos-android.md#c_psdk_signaling-mode-metadata-combos-android).

Ricorda quanto segue:

* Quando il server non restituisce un valore `AdBreaks` valido, TVSDK genera ed elabora un valore `NOPTimelineOperation` per l&#39;AdBreak vuoto e nessun annuncio viene riprodotto.

* Anche se C3 ad delete/substitution è destinato a essere supportato solo per VOD, se specificato nei metadati dell&#39;annuncio, gli intervalli di tempo vengono elaborati anche per i flussi in diretta.

