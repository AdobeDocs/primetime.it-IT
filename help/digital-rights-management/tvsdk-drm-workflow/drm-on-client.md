---
title: DRM Primetime sul client
description: DRM Primetime sul client
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 0%

---

# DRM Primetime sul client{#primetime-drm-on-the-client}

Un’applicazione TVSDK Primetime che riproduce contenuti protetti deve prima chiamare le API DRM Primetime per avviare il flusso di lavoro per l’utilizzo delle licenze e la riproduzione di contenuti protetti. In questo flusso di lavoro, Primetime DRM sul client crea una richiesta di licenza dai metadati del contenuto protetto, quindi la invia al server licenze Primetime DRM.

Prima di rilasciare la richiesta di licenza, il cliente può facoltativamente eseguire l’autenticazione/autorizzazione necessaria (a seconda delle regole aziendali).
