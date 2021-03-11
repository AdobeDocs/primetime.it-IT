---
description: Un generatore di opportunità identifica le opportunità di posizionamento tramite tag personalizzati in un flusso, marcatori personalizzati in modalità di segnalazione annunci e così via. Il generatore di opportunità invia queste opportunità di posizionamento al risolutore dei contenuti, che personalizza il flusso di lavoro di inserimento di contenuti/annunci in base alle proprietà e ai metadati dell’opportunità di posizionamento.
title: Personalizzare i generatori di opportunità e i risolutori di contenuti
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---


# Panoramica {#customize-opportunity-generators-and-content-resolvers-overview}

Un generatore di opportunità identifica le opportunità di posizionamento tramite tag personalizzati in un flusso, marcatori personalizzati in modalità di segnalazione annunci e così via. Il generatore di opportunità invia queste opportunità di posizionamento al risolutore dei contenuti, che personalizza il flusso di lavoro di inserimento di contenuti/annunci in base alle proprietà e ai metadati dell’opportunità di posizionamento.

TVSDK include i seguenti generatori di opportunità predefiniti:

* `ManifestCuesOpportunityGenerator` genera opportunità dai suggerimenti annunci predefiniti (  `#EXT-X-CUE`).

* `AdSignalingModeOpportunityGenerator` genera un’opportunità iniziale per la modalità di segnalazione degli annunci specificata. Questo ignora eventuali indizi o informazioni sui metadati temporizzati.
* `CustomMarkerOpportunityGenerator` genera opportunità per sostituire gli annunci C3 cotti-in.
* `AuditudeResolver`Il generatore di opportunità produce opportunità quando la risoluzione di annunci pigri è attiva.

TVSDK include anche i risolutori di contenuti predefiniti:

* `CustomRangeResolver`
* `JSONResolver`
* `AuditudeResolver`, che può comunicare con Primetime ad decision.

È possibile ignorare i generatori di opportunità e i risolutori di contenuti predefiniti per personalizzare il flusso di lavoro pubblicitario in modi come i seguenti:

* Riconoscere i tag personalizzati per l’inserimento di annunci
* Crea un provider di annunci personalizzato.
* Contenuto in nero.