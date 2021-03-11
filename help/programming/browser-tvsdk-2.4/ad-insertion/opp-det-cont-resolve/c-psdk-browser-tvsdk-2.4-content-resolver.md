---
description: Un rilevatore di opportunità è un componente browser TVSDK che rileva i tag personalizzati in un flusso e identifica le opportunità di posizionamento. Queste opportunità vengono inviate al risolutore dei contenuti, che personalizza il flusso di lavoro di inserimento di contenuti/annunci in base alle proprietà delle opportunità di posizionamento e ai metadati.
title: Personalizzare i rilevatori di opportunità e i risolutori di contenuti
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---


# Panoramica {#customize-opportunity-detectors-and-content-resolvers-overview}

Un rilevatore di opportunità è un componente browser TVSDK che rileva i tag personalizzati in un flusso e identifica le opportunità di posizionamento. Queste opportunità vengono inviate al risolutore dei contenuti, che personalizza il flusso di lavoro di inserimento di contenuti/annunci in base alle proprietà delle opportunità di posizionamento e ai metadati.

Il browser TVSDK include i seguenti rilevatori di opportunità predefiniti:

* `AdSignalingModeOpportunityGenerator`, che crea opportunità di posizionamento iniziale degli annunci in base alla modalità di segnalazione degli annunci.
* `ManifestCuesOpportunityGenerator`, che crea opportunità di posizionamento di annunci da qualsiasi tag di uscita di testo.

Il browser TVSDK include anche resolver di contenuti predefiniti, come `AuditudeResolver`, che fornisce contenuti che verranno inseriti in base alla chiave di metadati nell&#39;elemento del lettore. `AuditudeResolver` è in grado di comunicare con i server di ad decisioning di Adobe Primetime e di restituire interruzioni pubblicitarie da inserire.

È possibile ignorare i rilevatori di opportunità e i risolutori di contenuti predefiniti per personalizzare il flusso di lavoro pubblicitario nei seguenti modi:

* Aggiungi supporto per il rilevamento tag personalizzato
* Riconoscere i tag personalizzati per l’inserimento di annunci
* Creare un provider di annunci personalizzato

