---
description: Un rilevatore di opportunità è un componente Browser TVSDK che rileva i tag personalizzati in un flusso e identifica le opportunità di posizionamento. Queste opportunità vengono inviate al risolutore dei contenuti, che personalizzerà il flusso di lavoro di inserimento dei contenuti/annunci in base alle proprietà delle opportunità di posizionamento e ai metadati.
seo-description: Un rilevatore di opportunità è un componente Browser TVSDK che rileva i tag personalizzati in un flusso e identifica le opportunità di posizionamento. Queste opportunità vengono inviate al risolutore dei contenuti, che personalizzerà il flusso di lavoro di inserimento dei contenuti/annunci in base alle proprietà delle opportunità di posizionamento e ai metadati.
seo-title: Personalizzare rilevatori di opportunità e risolutori di contenuti
title: Personalizzare rilevatori di opportunità e risolutori di contenuti
uuid: d4926933-5966-4cd8-8050-c81c5e3c8545
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 0%

---


# Panoramica {#customize-opportunity-detectors-and-content-resolvers-overview}

Un rilevatore di opportunità è un componente Browser TVSDK che rileva i tag personalizzati in un flusso e identifica le opportunità di posizionamento. Queste opportunità vengono inviate al risolutore dei contenuti, che personalizzerà il flusso di lavoro di inserimento dei contenuti/annunci in base alle proprietà delle opportunità di posizionamento e ai metadati.

Il browser TVSDK include i seguenti rilevatori di opportunità predefiniti:

* `AdSignalingModeOpportunityGenerator`, che crea opportunità iniziali di posizionamento degli annunci in base alla modalità di segnalazione degli annunci.
* `ManifestCuesOpportunityGenerator`, che crea opportunità di posizionamento degli annunci da qualsiasi tag di giunzione.

Browser TVSDK include anche i risolutori di contenuto predefiniti, come `AuditudeResolver`, che forniscono il contenuto che verrà inserito in base alla chiave di metadati nell&#39;elemento del lettore. `AuditudeResolver` è in grado di comunicare con  server Adobe Primetime e di decidere gli annunci e di restituire le interruzioni da inserire.

Potete ignorare i rilevatori di opportunità e i risolutori di contenuti predefiniti per personalizzare il flusso di lavoro pubblicitario nei seguenti modi:

* Supporto aggiuntivo per il rilevamento tag personalizzato
* Riconoscere i tag personalizzati per l&#39;inserimento di annunci
* Creare un provider di annunci personalizzato

