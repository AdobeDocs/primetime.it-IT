---
description: È possibile utilizzare le funzioni del Digital Rights Management Primetime (DRM) per fornire un accesso sicuro ai contenuti video. In alternativa, è possibile utilizzare soluzioni DRM di terze parti come alternativa alla soluzione DRM integrata di Adobe di Primetime.
keywords: DRM;DASH;HLS
title: Panoramica dell'interfaccia DRM di Primetime
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---


# Panoramica dell&#39;interfaccia DRM di Primetime {#primetime-drm-interface-overview}

È possibile utilizzare le funzioni del Digital Rights Management Primetime (DRM) per fornire un accesso sicuro ai contenuti video. In alternativa, è possibile utilizzare soluzioni DRM di terze parti come alternativa alla soluzione DRM integrata di Adobe di Primetime.

<!--<a id="section_4DD54E085AB345FE9BE00865E56B28DB"></a>-->

Rivolgiti al tuo rappresentante di Adobe per ottenere informazioni aggiornate sulla disponibilità di soluzioni DRM di terze parti.

L&#39;elemento chiave lato client del sistema DRM (Digital Rights Management) di Primetime è il DRM Manager.

Primetime DRM fornisce un flusso di lavoro scalabile ed efficiente per implementare la protezione dei contenuti nelle applicazioni TVSDK. È possibile proteggere e gestire i diritti relativi ai contenuti video creando una licenza per ogni file multimediale digitale.

TVSDK supporta l’integrazione DRM di Primetime come flussi di lavoro DRM personalizzati. Ciò significa che l&#39;applicazione deve implementare i flussi di lavoro di autenticazione DRM prima di riprodurre il flusso utilizzando il Flash DRMManager. Per abilitare questo, MediaPlayer ti fornisce il gestore DRM per l&#39;autenticazione.

Fai riferimento al codice del sample player DRM incluso nel pacchetto TVSDK.

Questi sono gli elementi API più importanti per lavorare con DRM:

* Un riferimento nel lettore multimediale all&#39;oggetto manager DRM che implementa il sottosistema DRM:

   ```
   @property (readonly, nonatomic) DRMManager *drmManager
   ```

<!--<a id="section_F986DB1EDD6F44CD8E57419CCA0921E8"></a>-->

TVSDK invia una notifica `PTMediaPlayerItemDRMMetadataChanged` quando i metadati DRM cambiano. Questi metadati vengono utilizzati come input per quasi tutte le funzioni della classe `DRMManager`.

<!--<a id="section_223DCF63BAB6438792A85352A79044CC"></a>-->

Se il flusso protetto da DRM è codificato a bit rate multiplo (MBR), i metadati DRM utilizzati per la playlist di varianti devono essere gli stessi dei metadati utilizzati in tutti i flussi di bit rate.

>[!TIP]
>
>Quando fai riferimento agli URL delle risorse protette da DRM nell’app iOS, il parametro della stringa di query `?faxs=1` deve essere aggiunto all’URL M3U8 a livello di set (MBR). Ad esempio:

```
https://your.domain.com/hls/[...]/index.m3u8?faxs=1
```

Il parametro della stringa di query `faxs=1` segnala che il contenuto è protetto da DRM e attiva di conseguenza il flusso di lavoro di decrittografia DRM nel TVSDK iOS. Puoi anche aggiungere il tag `faxs=1` agli URL delle risorse HLS protette da DRM destinati ad altre piattaforme; viene osservato come richiesto su iOS o trattato come non-op in lettori su altre piattaforme.

## Implementare DRM di Primetime in un&#39;applicazione TSVDK {#implement-primetime-drm-in-a-tsvdk-application}

Primetime DRM è integrato in TVSDK, che semplifica l&#39;implementazione della protezione dei contenuti in un&#39;applicazione TVSDK.

Per una panoramica sull’utilizzo di DRM di Primetime per implementare la protezione dei contenuti in un’applicazione TVSDK, vedi:

* [Flusso di lavoro Adobe Primetime TVSDK-DRM (PDF)](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_tvsdk_drm_workflow.pdf)