---
description: Un generatore di opportunità identifica le opportunità di posizionamento tramite tag personalizzati in un flusso, indicatori personalizzati in modalità di segnalazione degli annunci e così via. Il generatore di opportunità invia queste opportunità di posizionamento al risolutore contenuti, che personalizza il flusso di lavoro di inserimento di contenuti/annunci in base alle proprietà e ai metadati dell’opportunità di posizionamento.
title: Personalizzare i generatori di opportunità e i risolutori di contenuti
exl-id: 5d0ebaa6-4708-4602-b9d7-882c389fb030
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---

# Panoramica {#customize-opportunity-generators-and-content-resolvers-overview}

Un generatore di opportunità identifica le opportunità di posizionamento tramite tag personalizzati in un flusso, indicatori personalizzati in modalità di segnalazione degli annunci e così via. Il generatore di opportunità invia queste opportunità di posizionamento al risolutore contenuti, che personalizza il flusso di lavoro di inserimento di contenuti/annunci in base alle proprietà e ai metadati dell’opportunità di posizionamento.

TVSDK include i seguenti generatori di opportunità predefiniti:

* `ManifestCuesOpportunityGenerator` genera opportunità dai segnali pubblicitari predefiniti ( `#EXT-X-CUE`).

* `AdSignalingModeOpportunityGenerator` genera un&#39;opportunità iniziale per la modalità di segnalazione dell&#39;annuncio specificata. Questa operazione ignora qualsiasi informazione sui segnali o sui metadati temporizzati.
* `CustomMarkerOpportunityGenerator` genera opportunità per sostituire gli annunci C3 infornati.
* `AuditudeResolver`Il generatore di opportunità di crea opportunità quando è attiva la risoluzione degli annunci pigri.

TVSDK include anche i resolver di contenuto predefiniti:

* `CustomRangeResolver`
* `JSONResolver`
* `AuditudeResolver`, che può comunicare con Primetime ad decisioning.

Puoi sovrascrivere i generatori di opportunità e i risolutori di contenuto predefiniti per personalizzare il flusso di lavoro per la pubblicità in modi quali i seguenti:

* Riconoscere tag personalizzati per l’inserimento di annunci. Per ulteriori informazioni, consulta [Personalizzare i generatori di opportunità e i risolutori di contenuti](../../../../tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/content-resolver/android-3x-content-resolver.md).
* Crea un provider di annunci personalizzato.
* Contenuto in blackout.
