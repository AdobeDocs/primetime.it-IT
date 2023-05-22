---
title: DRM Primetime sul client
description: DRM Primetime sul client
copied-description: true
exl-id: 157d558f-3014-4d05-bba1-e73134cedc23
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 0%

---

# DRM Primetime sul client{#primetime-drm-on-the-client}

Un’applicazione TVSDK Primetime che riproduce contenuti protetti deve prima chiamare le API DRM Primetime per avviare il flusso di lavoro per l’utilizzo delle licenze e la riproduzione di contenuti protetti. In questo flusso di lavoro, Primetime DRM sul client crea una richiesta di licenza dai metadati del contenuto protetto, quindi la invia al server licenze Primetime DRM.

Prima di rilasciare la richiesta di licenza, il cliente può facoltativamente eseguire l’autenticazione/autorizzazione necessaria (a seconda delle regole aziendali).
