---
description: TVSDK gestisce gli errori dell'intervallo di tempo in base al problema specifico unendo o riordinando gli intervalli di tempo definiti in modo errato.
seo-description: TVSDK gestisce gli errori dell'intervallo di tempo in base al problema specifico unendo o riordinando gli intervalli di tempo definiti in modo errato.
seo-title: Gestione degli errori di aggiunta ed eliminazione
title: Gestione degli errori di aggiunta ed eliminazione
uuid: 9a951bc4-b372-4655-8510-3f474171415d
translation-type: tm+mt
source-git-commit: 21d1eae53cea303221de00765724e787cf6e84ef

---


# Panoramica {#ad-deletion-and-replacement-error-handling-overview}

TVSDK gestisce gli errori dell&#39;intervallo di tempo in base al problema specifico unendo o riordinando gli intervalli di tempo definiti in modo errato.

TVSDK gestisce `timeRanges` gli errori tramite l&#39;unione e il riordinamento predefiniti dei processi. In primo luogo, il giocatore ordina intervalli di tempo definiti dal cliente per l&#39;ora di *inizio* . In base a questo ordine di ordinamento, in presenza di sottoinsiemi e intersezioni tra gli intervalli, TVSDK unisce gli intervalli adiacenti e unisce questi intervalli.

TVSDK gestisce gli errori relativi all’intervallo di tempo con le seguenti opzioni:

* **TVSDK non ordinato** riordina gli intervalli di tempo.

* **Subset** TVSDK unisce i sottoinsiemi dell’intervallo di tempo.

* **Interseca** TVSDK unisce gli intervalli di tempo intersecanti.

* **L’SDK per la sostituzione di intervalli in conflitto** consente di selezionare la durata della sostituzione dal primo `timeRange` che viene visualizzato nel gruppo in conflitto.

TVSDK gestisce i conflitti in modalità di segnalazione con i metadati degli annunci nei seguenti modi:

* Se la modalità di segnalazione degli annunci è in conflitto con i metadati dell&#39;intervallo di tempo, i metadati dell&#39;intervallo di tempo hanno sempre la priorità.

   Ad esempio, se la modalità di segnalazione degli annunci è impostata come segnali di manifesto o mappa del server e nei metadati degli annunci sono presenti anche intervalli di tempo MARK, il comportamento risultante è che gli intervalli sono contrassegnati e non vengono inseriti annunci.
* Per gli intervalli REPLACE, se la modalità di segnalazione è impostata come segnale di manifesto o mappa del server, gli intervalli vengono sostituiti come specificato negli intervalli REPLACE e non vi è inserimento di annunci tramite la mappa del server o segnali di manifesto.

   Per ulteriori informazioni, consulta la tabella *Modalità di segnalazione/Combinazione di metadati Comportamenti* in [Effetto sull’inserimento e l’eliminazione di annunci dalla modalità di segnalazione...](../../../../tvsdk-2.7-for-android/ad-insertion/delete-replace-content-vod/c-psdk-android-2.7-signaling-mode-metadata-combos-android.md#c_psdk_signaling-mode-metadata-combos-android).

Ricorda quanto segue:

* Se il server non restituisce un valore valido `AdBreaks`, TVSDK genera ed elabora un `NOPTimelineOperation` valore per AdBreak vuoto e nessun annuncio viene riprodotto.

* Anche se C3 ed delete/replace è destinato a essere supportato solo per VOD, se specificato nei metadati dell&#39;annuncio, anche gli intervalli di tempo vengono elaborati per i flussi live.

