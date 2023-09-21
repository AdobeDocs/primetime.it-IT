---
description: L'elemento chiave lato client del sistema DRM (Digital Rights Management) di Primetime è DRM Manager.
title: Panoramica dell’interfaccia DRM di Primetime
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---

# Panoramica dell’interfaccia DRM di Primetime{#primetime-drm-interface-overview}

L&#39;elemento chiave lato client del sistema DRM (Digital Rights Management) di Primetime è DRM Manager.

<!--<a id="section_4DD54E085AB345FE9BE00865E56B28DB"></a>-->

Primetime DRM fornisce un flusso di lavoro scalabile ed efficiente per implementare la protezione dei contenuti nelle applicazioni TVSDK. Per proteggere e gestire i diritti dei contenuti video, crea una licenza per ciascun file multimediale digitale.

TVSDK supporta l’integrazione di Primetime DRM come flussi di lavoro DRM personalizzati. Ciò significa che l&#39;applicazione deve implementare i flussi di lavoro di autenticazione DRM prima di riprodurre il flusso utilizzando il Flash `DRMManager`. Per abilitare questa funzione, `MediaPlayer` fornisce DRM Manager per l&#39;autenticazione.

Questi sono gli elementi API più importanti per l’utilizzo di DRM:

* Riferimento nel lettore multimediale all&#39;oggetto di gestione DRM che implementa il sottosistema DRM:

  ```
  public function get drmManager():DRMManager 
  ```

<!--<a id="section_4204CE2731A44F67A3664AEDE8CCCA47"></a>-->

Elementi API rilevanti aggiuntivi:

* [flash.net.drm.DRMManager](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/net/drm/DRMManager.html)
* [flash.net.drm.DRMContentData](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/net/drm/DRMContentData.html)
* [flash.net.drm.DRMVoucher](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/net/drm/DRMVoucher.html)
* [flash.net.drm.AuthenticationMethod](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/net/drm/AuthenticationMethod.html)
* [flash.events.DRMStatusEvent](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/events/DRMStatusEvent.html)
* [flash.events.DRMErrorEvent](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/events/DRMErrorEvent.html)

<!--<a id="section_F58941D68EB94A5EBD1C7454D2A1B17A"></a>-->

Per ulteriori informazioni su DRM, consultare la documentazione di Adobe Primetime DRM.
