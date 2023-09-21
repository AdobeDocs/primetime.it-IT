---
description: L'elemento chiave lato client del sistema DRM (Digital Rights Management) di Primetime è DRM Manager.
title: Panoramica dell’interfaccia DRM di Primetime
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 0%

---

# Panoramica dell’interfaccia DRM di Primetime {#primetime-drm-interface-overview}

È possibile utilizzare le funzioni del Digital Rights Management Primetime (DRM) per fornire un accesso sicuro al contenuto video. In alternativa, è possibile utilizzare soluzioni DRM di terze parti in alternativa alla soluzione DRM di Primetime integrata di Adobe.

Per informazioni aggiornate sulla disponibilità di soluzioni DRM di terze parti, rivolgersi al proprio rappresentante di Adobe.

L&#39;elemento chiave lato client del sistema DRM (Digital Rights Management) di Primetime è DRM Manager.

<!--<a id="section_4DD54E085AB345FE9BE00865E56B28DB"></a>-->

Primetime DRM fornisce un flusso di lavoro scalabile ed efficiente per implementare la protezione dei contenuti nelle applicazioni TVSDK. Per proteggere e gestire i diritti dei contenuti video, crea una licenza per ciascun file multimediale digitale.

TVSDK supporta l’integrazione di Primetime DRM come flussi di lavoro DRM personalizzati. Ciò significa che l&#39;applicazione deve implementare i flussi di lavoro di autenticazione DRM prima di riprodurre il flusso utilizzando DRMManager di Flash. Per attivare questa opzione, MediaPlayer fornisce il gestore DRM per l&#39;autenticazione.

Consulta il codice del sample player DRM incluso nel pacchetto TVSDK.

Questi sono gli elementi API più importanti per l’utilizzo di DRM:

* Riferimento nel lettore multimediale all&#39;oggetto di gestione DRM che implementa il sottosistema DRM:

  ```
  @property (readonly, nonatomic) DRMManager *drmManager
  ```

<!--<a id="section_F986DB1EDD6F44CD8E57419CCA0921E8"></a>-->

Problemi TVSDK a `PTMediaPlayerItemDRMMetadataChanged` notifica quando i metadati DRM cambiano. Questi metadati vengono utilizzati come input per quasi tutte le funzioni del `DRMManager` classe.

<!--<a id="section_223DCF63BAB6438792A85352A79044CC"></a>-->

Se lo streaming protetto da DRM è codificato con bit rate multiplo (MBR), i metadati DRM utilizzati per la playlist delle varianti devono essere gli stessi dei metadati utilizzati in tutti i flussi di bit rate.

>[!TIP]
>
>Quando si fa riferimento agli URL delle risorse protette da DRM nell’app iOS, il parametro della stringa di query `?faxs=1` deve essere aggiunto all’URL M3U8 del livello set (MBR). Ad esempio:
>
>```
>https://your.domain.com/hls/[...]/index.m3u8?faxs=1
>```
>
>Il `faxs=1` il parametro della stringa di query segnala che il contenuto è protetto da DRM e attiva di conseguenza il flusso di lavoro di decrittografia DRM in iOS TVSDK. Puoi anche aggiungere `faxs=1` tag sugli URL delle risorse HLS protetti da DRM destinati ad altre piattaforme; viene osservato come richiesto su iOS o trattato come non-op nei lettori su altre piattaforme.

<!--<a id="section_F58941D68EB94A5EBD1C7454D2A1B17A"></a>-->

Per ulteriori informazioni su DRM, vedere [Documentazione di Adobe Primetime DRM](https://help.adobe.com/en_US/primetime/drm).

## Implementare Primetime DRM in un&#39;applicazione TSVDK {#implement-primetime-drm-in-a-tsvdk-application}

Primetime DRM è integrato in TVSDK, il che semplifica l’implementazione della protezione dei contenuti in un’applicazione TVSDK.

Per una panoramica e dettagli sull’utilizzo di Primetime DRM per implementare la protezione dei contenuti in un’applicazione TVSDK, consulta:

* [Flusso di lavoro Adobe Primetime TVSDK-DRM (PDF)](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_tvsdk_drm_workflow.pdf)
