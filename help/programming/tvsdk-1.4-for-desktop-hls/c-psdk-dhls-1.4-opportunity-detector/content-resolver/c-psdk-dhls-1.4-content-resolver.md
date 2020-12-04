---
description: Un rilevatore di opportunità è un componente TVADK che rileva i tag personalizzati in un flusso e identifica le opportunità di posizionamento. Queste opportunità vengono inviate al risolutore dei contenuti, che personalizzerà il flusso di lavoro di inserimento dei contenuti/annunci in base alle proprietà delle opportunità di posizionamento e ai metadati.
seo-description: Un rilevatore di opportunità è un componente TVADK che rileva i tag personalizzati in un flusso e identifica le opportunità di posizionamento. Queste opportunità vengono inviate al risolutore dei contenuti, che personalizzerà il flusso di lavoro di inserimento dei contenuti/annunci in base alle proprietà delle opportunità di posizionamento e ai metadati.
seo-title: Personalizzare rilevatori di opportunità e risolutori di contenuti
title: Personalizzare rilevatori di opportunità e risolutori di contenuti
uuid: 7bd04c8f-6f04-4321-88e8-9bb93251d940
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---


# Panoramica {#customize-opportunity-detectors-and-content-resolvers-overiew}

Un rilevatore di opportunità è un componente TVADK che rileva i tag personalizzati in un flusso e identifica le opportunità di posizionamento. Queste opportunità vengono inviate al risolutore dei contenuti, che personalizzerà il flusso di lavoro di inserimento dei contenuti/annunci in base alle proprietà delle opportunità di posizionamento e ai metadati.

TVSDK include rilevatori di opportunità predefiniti:

* `SpliceOutOpportunityDetector`, che comprende i segnali di annunci predefiniti
* `AdSignalingModeOpportunityGenerator`, responsabile della creazione di opportunità di inserimento iniziale degli annunci in base alla modalità di segnalazione degli annunci
* `SpliceOutOpportunityGenerator`, responsabile della creazione di opportunità di posizionamento degli annunci da qualsiasi tag #EXT-X-CUE

TVSDK include anche un risolutore di contenuto predefinito che fornisce il contenuto da inserire in base alla chiave di metadati nell&#39;elemento del lettore:

* `AuditudeResolver`, in grado di comunicare con  server di annunci pubblicitari Adobe Primetime (precedentemente noti come Auditude) e di restituire interruzioni pubblicitarie da inserire.

Potete ignorare i rilevatori di opportunità e i risolutori di contenuti predefiniti per personalizzare il flusso di lavoro pubblicitario nei seguenti modi:

* Supporto aggiuntivo per il rilevamento tag personalizzato
* Riconoscere i tag personalizzati per l&#39;inserimento di annunci
* Creare un provider di annunci personalizzato
* Contenuto BlackOut

