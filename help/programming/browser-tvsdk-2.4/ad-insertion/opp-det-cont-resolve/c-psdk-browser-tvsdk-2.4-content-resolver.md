---
description: Un rilevatore di opportunità è un componente TVSDK del browser che rileva i tag personalizzati in un flusso e identifica le opportunità di posizionamento. Queste opportunità vengono inviate al resolver dei contenuti, che personalizza il flusso di lavoro di inserimento di contenuti/annunci in base alle proprietà e ai metadati dell’opportunità di posizionamento.
title: Personalizzare i rilevatori di opportunità e i risolutori di contenuti
exl-id: 1866ed53-acfc-45d3-941e-0ed171aa038b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---

# Panoramica {#customize-opportunity-detectors-and-content-resolvers-overview}

Un rilevatore di opportunità è un componente TVSDK del browser che rileva i tag personalizzati in un flusso e identifica le opportunità di posizionamento. Queste opportunità vengono inviate al resolver dei contenuti, che personalizza il flusso di lavoro di inserimento di contenuti/annunci in base alle proprietà e ai metadati dell’opportunità di posizionamento.

Il TVSDK del browser include i seguenti rilevatori di opportunità predefiniti:

* `AdSignalingModeOpportunityGenerator`, che crea opportunità di posizionamento pubblicitario iniziale in base alla modalità di segnalazione degli annunci.
* `ManifestCuesOpportunityGenerator`, che crea opportunità di posizionamento di annunci da qualsiasi tag di giunzione.

Il TVSDK del browser include anche i risolutori di contenuto predefiniti, come `AuditudeResolver`, che fornisce contenuti che verranno inseriti in base alla chiave dei metadati nell’elemento del lettore. `AuditudeResolver` è in grado di comunicare con i server di Adobe Primetime ad decisioning e di restituire le interruzioni pubblicitarie da inserire.

Puoi sovrascrivere i rilevatori di opportunità e i risolutori di contenuto predefiniti per personalizzare il flusso di lavoro della pubblicità nei seguenti modi:

* Aggiunta del supporto per il rilevamento di tag personalizzati
* Riconoscere tag personalizzati per l’inserimento di annunci
* Creare un provider di annunci personalizzato
