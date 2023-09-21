---
description: Un rilevatore di opportunità è un componente TVADK che rileva i tag personalizzati in un flusso e identifica le opportunità di posizionamento. Queste opportunità vengono inviate al resolver dei contenuti, che personalizza il flusso di lavoro di inserimento di contenuti/annunci in base alle proprietà e ai metadati dell’opportunità di posizionamento.
title: Personalizzare i rilevatori di opportunità e i risolutori di contenuti
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---

# Panoramica {#customize-opportunity-detectors-and-content-resolvers-overiew}

Un rilevatore di opportunità è un componente TVADK che rileva i tag personalizzati in un flusso e identifica le opportunità di posizionamento. Queste opportunità vengono inviate al resolver dei contenuti, che personalizza il flusso di lavoro di inserimento di contenuti/annunci in base alle proprietà e ai metadati dell’opportunità di posizionamento.

TVSDK include i rilevatori di opportunità predefiniti:

* `SpliceOutOpportunityDetector`, che comprende i suggerimenti per annunci predefiniti
* `AdSignalingModeOpportunityGenerator`, responsabile della creazione di opportunità di annuncio iniziali in base alla modalità di segnalazione degli annunci
* `SpliceOutOpportunityGenerator`, responsabile della creazione di opportunità di annuncio da qualsiasi tag #EXT-X-CUE

TVSDK include anche un risolutore contenuto predefinito che fornisce contenuto da inserire in base alla chiave dei metadati nell’elemento del lettore:

* `AuditudeResolver`, in grado di comunicare con i server di Adobe Primetime ad decisioning (precedentemente noti come Auditude) e di restituire le interruzioni pubblicitarie da inserire.

Puoi sovrascrivere i rilevatori di opportunità e i risolutori di contenuto predefiniti per personalizzare il flusso di lavoro della pubblicità nei seguenti modi:

* Aggiunta del supporto per il rilevamento di tag personalizzati
* Riconoscere tag personalizzati per l’inserimento di annunci
* Creare un provider di annunci personalizzato
* Contenuto in black out
