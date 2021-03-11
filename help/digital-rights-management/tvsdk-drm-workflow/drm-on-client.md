---
title: DRM di Primetime sul client
description: DRM di Primetime sul client
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 0%

---


# DRM di Primetime sul client{#primetime-drm-on-the-client}

Un’applicazione TVSDK di Primetime che riproduce contenuto protetto deve prima chiamare le API DRM di Primetime per avviare il flusso di lavoro per il consumo di licenze e la riproduzione di contenuti protetti. In questo flusso di lavoro, Primetime DRM sul client costruisce una richiesta di licenza dai metadati del contenuto protetto, quindi la invia al server di licenze DRM di Primetime.

Prima di rilasciare la richiesta di licenza, il cliente può eseguire facoltativamente l&#39;autenticazione/autorizzazione necessarie (a seconda delle tue regole aziendali).
