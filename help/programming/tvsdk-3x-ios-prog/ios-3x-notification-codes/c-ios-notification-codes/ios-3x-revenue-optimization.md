---
description: 'Questa tabella fornisce informazioni dettagliate sulle notifiche di ottimizzazione delle entrate. '
seo-description: 'Questa tabella fornisce informazioni dettagliate sulle notifiche di ottimizzazione delle entrate. '
seo-title: Codice di ottimizzazione REVENUE
title: Codice di ottimizzazione REVENUE
translation-type: tm+mt
source-git-commit: df3d60874701383325be1afdd1ec5fe036f855f8
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 0%

---


# Codice di ottimizzazione REVENUE {#revenue-optimization-code}

Questa tabella fornisce informazioni dettagliate sulle notifiche di OTTIMIZZAZIONE DELLE ENTRATE.

## Abilita report ottimizzazione ricavi {#enable-revenue-optimization-reporting}

Per abilitare questo rapporto, usa l’API PTMediaPlayer: `[mediaPlayersetRevenueOptimizationReportingLevel:PTNotificationTypeInfo]`.

>[!NOTE]
>
>La maggior parte delle notifiche informative contiene metadati rilevanti, ad esempio l’URL della risorsa che non è stato possibile scaricare. Alcune notifiche contengono metadati per specificare se il problema si è verificato nel contenuto video principale, nel contenuto audio alternativo o in un annuncio.

| Code | Nome | Notifica interna | Tasti metadati | Commenti |
|---|---|---|---|---|
| 401001 | REVENUE_OPTIMIZATION_REPORTING | None | Per le chiavi dei metadati basate su eventi diversi, consultate la tabella seguente. | None |

| Dettagli evento | ContextMetadata |
|---|---|
| **CONTENT_RESOURCE_** STARTDispatched in TVSDK quando viene chiamato MediaPlayer::replaceCurrentResource. | clientTimestamp, fallbackOnInvalidCreative, showStaticBanners, hasPreroll, event, adSignalingMode, resourceUrl, creativeRepackageFormat, delayAdLoadingTolerance, zoneID, hasLivePreroll, adRequestTimeout, delayAdLoading, resourceType, creativeRepackageEnabled, mediaId, clientId |
| **CONTENT_PLAYBACK_** STARTDispatched in TVSDK quando il contenuto è entrato nello stato preparato ed è pronto per la riproduzione. Questo evento non verrà inviato su ogni caricamento del manifesto; verrà inviato solo sul caricamento iniziale. | clientTimestamp, contentURL, contentType, event, isLive, clientID |
| **AD_OPPORTUNITY_** GENERATEDDispatched in TVSDK quando viene generata un&#39;opportunità. | clientTimestamp, evento, opportunitàId, placementDuration, clientId |
| **AD_OPPORTUNITY_RESOLVE_** STARTDinviato in TVSDK quando inizia la risoluzione di un&#39;opportunità. | clientTimestamp, evento, opportunitàId, placementDuration, clientId |
| **AD_OPPORTUNITY_RESOLVE_** FAILEDDinviato in TVSDK quando un risolutore di annunci chiama MediaPlayerClient::notificationFailed(). Necessità di compilare i dati | opportunitàId, notificationAD |
| **AD_RESOURCE_** LOADDispatched quando una qualsiasi risorsa annuncio viene recuperata dall&#39;URL. responseStartTime:marca temporale Unix per la prima volta che è iniziata la richiesta. responseTotalTime:quantità totale di tempo (in secondi) necessario per il caricamento di una risposta. responseStatus: il codice di stato rilevato durante il recupero della risorsa. status:&quot;error&quot; o &quot;success&quot; referrerAdId: l&#39;ID dell&#39;annuncio di provenienza che ha richiesto il recupero di questa risorsa (se presente). referrerUrl: l&#39;URL di provenienza del quale è stato richiesto il recupero della risorsa. errorMessage:Se lo stato è &quot;error&quot;, il motivo dell&#39;errore si trova qui. | experienceId, resourceType, responseTotalTime, responseStatus, responseStartTime, stato, errorMessage, url, referrerURL, referrerAdId |
| **AD_RESOURCE_LOAD_** CRSDinviato in TVSDK quando un CRS viene applicato a una risorsa, così come la risposta per m3u8. resourceType:always &quot;crs&quot;. responseStartTime:marca temporale Unix per la prima volta che è iniziata la richiesta. responseTotalTime:quantità totale di tempo (in secondi) necessario per il caricamento di una risposta. responseStatus: il codice di stato rilevato durante il recupero della risorsa. status:&quot;error&quot; o &quot;success&quot;. errorMessage:Se lo stato è &quot;error&quot;, il motivo dell&#39;errore si trova qui. mediaFileUrl:L&#39;URL del file multimediale originale selezionato. mediaFileBitrate:bitrate del file multimediale selezionato. mediaFileMimeType: Il tipo mime del file multimediale selezionato. url:L’URL della risorsa finale. | opportunitàId, resourceType, responseTotalTime, responseStatus, responseStartTime, stato, errorMessage, url, mediaFileURL, mediaFileBitrate, mediaFileMimeType, url |
| **AD_TIMELINE_** PLACEDispatched in TVSDK dopo che un adBreak è stato inserito nella timeline. Questo evento si verificherà una volta per ogni interruzione di annuncio. propostoTime: l&#39;ora in cui è stata richiesta l&#39;interruzione dell&#39;annuncio. effectiveTime: l’ora in cui l’interruzione dell’annuncio è stata effettivamente inserita. durataProposta: durata dell&#39;interruzione annuncio richiesta per l&#39;inserimento. Per il contenuto live questo è il periodo di tempo previsto. Per il contenuto VOD si tratterebbe normalmente di -1. effectiveDuration: la durata effettiva dell&#39;interruzione annuncio inserita. Calcolato come la durata della somma di tutti gli annunci, definita dalle rispettive durate del segmento, aggiunti o sostituiti nella timeline del flusso originale. proposteAnnunci: il numero di annunci nell&#39;interruzione annuncio proposta. totalAds: il numero di annunci inseriti correttamente. annunci pubblicitari...n:Gli annunci inseriti correttamente verranno inseriti qui. È possibile recuperare informazioni complete e manifesto da AD_OPPORTUNITY_RESOLVE_PROCESS | opportunitàId, stato, errorMessage, averageTime, proposteDuration, effectiveTime, effectiveDuration, proposteAds, totalAds, ads_id, ads_type, ads_Duration, ads_url |
| **AD_PLAYBACK_** STARTDinviato in TVSDK dopo l&#39;inizio della riproduzione di un annuncio. | clientTimestamp, evento, id, url, durata, tipo, opportunitàId, clientId |
| **AD_PLAYBACK_** COMPLETEDspeched in TVSDK dopo che un annuncio ha completato la riproduzione. | clientTimestamp, evento, id, url, durata, tipo, opportunitàId, clientId |
| **ADBREAK_PLAYBACK_** STARTDispatched in TVSDK quando un&#39;interruzione di riga avvia la riproduzione. | clientTimestamp, evento, entityId opportunità, durata, ora, clientId |
| **ADBREAK_PLAYBACK_** COMPLETEDispatched in TVSDK quando una pausa termina la riproduzione. | clientTimestamp, evento, opportunitàId, clientId |
| **CONTENT_PLAYBACK_** COMPLETEDispatched in TVSDK quando viene completato un contenuto. Ciò potrebbe verificarsi se il flusso viene sostituito, il lettore immette uno stato di errore, il lettore viene reimpostato o il contenuto viene effettivamente completato. Questo evento sarà necessario per tenere traccia di sessionId. | clientTimestamp, evento, clientId, url, stato, errorMessage |
| **AD_PLAYBACK_** ERRORDispatched in TVSDK quando un annuncio presenta un errore durante la riproduzione (errori del flusso di variante). | evento, errore, timestamp, manifestUrl, ora, opportunitàId, url |
