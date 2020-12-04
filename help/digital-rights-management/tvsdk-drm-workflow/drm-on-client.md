---
seo-title: DRM di Primetime sul client
title: DRM di Primetime sul client
uuid: 472180ad-6596-4a24-aa51-7909a75a5e10
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 0%

---


# DRM di Primetime sul client{#primetime-drm-on-the-client}

Un’applicazione TVSDK Primetime che riproduce il contenuto protetto deve prima chiamare le API DRM Primetime per avviare il flusso di lavoro per il consumo di licenza e la riproduzione del contenuto protetto. In questo flusso di lavoro, Primetime DRM sul client crea una richiesta di licenza dai metadati del contenuto protetto, quindi la invia al server licenze Primetime DRM.

Prima di rilasciare la richiesta di licenza, il cliente può eseguire facoltativamente l&#39;autenticazione/l&#39;autorizzazione necessarie (a seconda delle regole aziendali).
