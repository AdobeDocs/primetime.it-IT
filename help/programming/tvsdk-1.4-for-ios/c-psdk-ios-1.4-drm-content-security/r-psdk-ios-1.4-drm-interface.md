---
description: L'elemento chiave lato client del sistema DRM (Digital Rights Management) di Primetime è il manager DRM.
seo-description: L'elemento chiave lato client del sistema DRM (Digital Rights Management) di Primetime è il manager DRM.
seo-title: Panoramica dell'interfaccia DRM di Primetime
title: Panoramica dell'interfaccia DRM di Primetime
uuid: 3aae7c7a-fd0c-430e-9018-fd72801ab778
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---


# Panoramica dell&#39;interfaccia DRM di Primetime {#primetime-drm-interface-overview}

Potete utilizzare le funzioni del sistema Digital Rights Management Primetime (DRM) per fornire un accesso sicuro ai contenuti video. In alternativa, è possibile utilizzare soluzioni DRM di terze parti come alternativa  soluzione DRM integrata di Primetime  Adobe.

Consultate il rappresentante del Adobe  per informazioni aggiornate sulla disponibilità di soluzioni DRM di terze parti.

L&#39;elemento chiave lato client del sistema DRM (Digital Rights Management) di Primetime è il manager DRM.

<!--<a id="section_4DD54E085AB345FE9BE00865E56B28DB"></a>-->

Primetime DRM fornisce un flusso di lavoro scalabile ed efficiente per implementare la protezione dei contenuti nelle applicazioni TVSDK. Potete proteggere e gestire i diritti relativi ai contenuti video creando una licenza per ciascun file multimediale digitale.

TVSDK supporta l&#39;integrazione DRM di Primetime come flussi di lavoro DRM personalizzati. Ciò significa che l&#39;applicazione deve implementare i flussi di lavoro di autenticazione DRM prima di riprodurre il flusso utilizzando il Flash DRMManager. Per attivare questa funzione, MediaPlayer offre la gestione DRM per l’autenticazione.

Fate riferimento al codice del lettore di esempio DRM incluso nel pacchetto TVSDK.

Questi sono gli elementi API più importanti per lavorare con DRM:

* Un riferimento nel lettore multimediale all&#39;oggetto manager DRM che implementa il sottosistema DRM:

   ```
   @property (readonly, nonatomic) DRMManager *drmManager
   ```

<!--<a id="section_F986DB1EDD6F44CD8E57419CCA0921E8"></a>-->

TVSDK invia una `PTMediaPlayerItemDRMMetadataChanged` notifica quando i metadati DRM vengono modificati. Questi metadati vengono utilizzati come input per quasi tutte le funzioni della `DRMManager` classe.

<!--<a id="section_223DCF63BAB6438792A85352A79044CC"></a>-->

Se il flusso protetto da DRM è codificato con bitrate multiplo (MBR), i metadati DRM utilizzati per la playlist variante devono essere identici ai metadati utilizzati in tutti i flussi di bit rate.

>[!TIP]
>
>Quando fate riferimento agli URL di risorse protetti da DRM nell&#39;app iOS, il parametro della stringa di query `?faxs=1` deve essere aggiunto all&#39;URL M3U8 (MBR) a livello di set. Ad esempio:
>
>
```
>https://your.domain.com/hls/[...]/index.m3u8?faxs=1
>```
>
>Il parametro della stringa di `faxs=1` query segnala che il contenuto è protetto da DRM e attiva il flusso di lavoro di decrittazione DRM di conseguenza in iOS TVSDK. Potete anche aggiungere il `faxs=1` tag sugli URL delle risorse HLS protette da DRM destinati ad altre piattaforme; viene osservato come richiesto su iOS o trattato come non-op in lettori su altre piattaforme.

<!--<a id="section_F58941D68EB94A5EBD1C7454D2A1B17A"></a>-->

Per ulteriori informazioni su DRM, consulta la [documentazione](https://help.adobe.com/en_US/primetime/drm)Adobe Primetime DRM.

## Implementare DRM Primetime in un’applicazione TSVDK {#implement-primetime-drm-in-a-tsvdk-application}

Primetime DRM è integrato in TVSDK, che semplifica l&#39;implementazione della protezione del contenuto in un&#39;applicazione TVSDK.

Per una panoramica e informazioni dettagliate sull’utilizzo di DRM Primetime per implementare la protezione dei contenuti in un’applicazione TVSDK, vedi:

* [Flusso di lavoro  Adobe Primetime TVSDK-DRM (PDF)](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_tvsdk_drm_workflow.pdf)