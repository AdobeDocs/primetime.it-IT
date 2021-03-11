---
description: Un rilevatore di opportunità è un componente TVADK che rileva i tag personalizzati in un flusso e identifica le opportunità di posizionamento. Queste opportunità vengono inviate al risolutore dei contenuti, che personalizza il flusso di lavoro di inserimento di contenuti/annunci in base alle proprietà delle opportunità di posizionamento e ai metadati.
title: Personalizzare i rilevatori di opportunità e i risolutori di contenuti
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---


# Panoramica {#customize-opportunity-detectors-and-content-resolvers-overiew}

Un rilevatore di opportunità è un componente TVADK che rileva i tag personalizzati in un flusso e identifica le opportunità di posizionamento. Queste opportunità vengono inviate al risolutore dei contenuti, che personalizza il flusso di lavoro di inserimento di contenuti/annunci in base alle proprietà delle opportunità di posizionamento e ai metadati.

TVSDK include i rilevatori di opportunità predefiniti:

* `SpliceOutOpportunityDetector`, che comprende i suggerimenti sugli annunci predefiniti
* `AdSignalingModeOpportunityGenerator`, responsabile della creazione di opportunità di posizionamento iniziale degli annunci in base alla modalità di segnalazione degli annunci
* `SpliceOutOpportunityGenerator`, responsabile della creazione di opportunità di posizionamento di annunci da qualsiasi tag #EXT-X-CUE

TVSDK include anche un risolutore di contenuti predefinito che fornisce il contenuto da inserire in base alla chiave di metadati nell&#39;elemento del lettore:

* `AuditudeResolver`, in grado di comunicare con i server di ad decisioning di Adobe Primetime (noti in precedenza come Auditude) e di restituire interruzioni pubblicitarie da inserire.

È possibile ignorare i rilevatori di opportunità e i risolutori di contenuti predefiniti per personalizzare il flusso di lavoro pubblicitario nei seguenti modi:

* Aggiungi supporto per il rilevamento tag personalizzato
* Riconoscere i tag personalizzati per l’inserimento di annunci
* Creare un provider di annunci personalizzato
* Contenuto in uscita

