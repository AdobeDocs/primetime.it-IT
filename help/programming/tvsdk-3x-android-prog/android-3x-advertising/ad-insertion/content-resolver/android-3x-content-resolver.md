---
description: Un generatore di opportunità identifica le opportunità di posizionamento tramite tag personalizzati in un flusso, marcatori personalizzati in modalità di segnalazione annunci e così via. Il generatore di opportunità invia queste opportunità di posizionamento al risolutore dei contenuti, che personalizzerà il flusso di lavoro di inserimento dei contenuti/annunci in base alle proprietà e ai metadati dell'opportunità di posizionamento.
seo-description: Un generatore di opportunità identifica le opportunità di posizionamento tramite tag personalizzati in un flusso, marcatori personalizzati in modalità di segnalazione annunci e così via. Il generatore di opportunità invia queste opportunità di posizionamento al risolutore dei contenuti, che personalizzerà il flusso di lavoro di inserimento dei contenuti/annunci in base alle proprietà e ai metadati dell'opportunità di posizionamento.
seo-title: Personalizzare i generatori di opportunità e i risolutori di contenuti
title: Personalizzare i generatori di opportunità e i risolutori di contenuti
uuid: 0d4fb0b2-98f3-4245-9bf1-4e968c5d0f36
translation-type: tm+mt
source-git-commit: ed910a60440ae7c0d19d9be56c80c8bdbc62bcf1

---


# Panoramica {#customize-opportunity-generators-and-content-resolvers-overview}

Un generatore di opportunità identifica le opportunità di posizionamento tramite tag personalizzati in un flusso, marcatori personalizzati in modalità di segnalazione annunci e così via. Il generatore di opportunità invia queste opportunità di posizionamento al risolutore dei contenuti, che personalizzerà il flusso di lavoro di inserimento dei contenuti/annunci in base alle proprietà e ai metadati dell&#39;opportunità di posizionamento.

TVSDK include i seguenti generatori di opportunità predefiniti:

* `ManifestCuesOpportunityGenerator` genera opportunità dai segnali di annunci predefiniti ( `#EXT-X-CUE`).

* `AdSignalingModeOpportunityGenerator` genera un&#39;opportunità iniziale per la modalità di segnalazione annunci specificata. In questo modo vengono ignorati eventuali suggerimenti o informazioni sui metadati temporizzati.
* `CustomMarkerOpportunityGenerator` genera opportunità per sostituire gli annunci C3 con un pacchetto.
* `AuditudeResolver`Il generatore di opportunità produce opportunità quando pigro e risoluzione è attivato.

TVSDK include anche i risolutori di contenuto predefiniti:

* `CustomRangeResolver`
* `JSONResolver`
* `AuditudeResolver`, in grado di comunicare con Primetime e le decisioni relative agli annunci.

Potete ignorare i generatori di opportunità e i risolutori di contenuti predefiniti per personalizzare il flusso di lavoro pubblicitario in modi quali:

* Riconosci tag personalizzati per l&#39;inserimento di annunci. Per ulteriori informazioni, consultate [Personalizzare i generatori di opportunità e i risolutori](../../../../tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/content-resolver/android-3x-content-resolver.md)di contenuti.
* Crea un fornitore di annunci personalizzato.
* Escludere il contenuto.