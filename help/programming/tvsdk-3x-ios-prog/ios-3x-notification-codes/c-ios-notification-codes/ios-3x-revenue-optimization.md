---
description: 'Questa tabella fornisce informazioni dettagliate sulle notifiche di ottimizzazione delle entrate. '
seo-description: 'Questa tabella fornisce informazioni dettagliate sulle notifiche di ottimizzazione delle entrate. '
seo-title: Codice di ottimizzazione REVENUE
title: Codice di ottimizzazione REVENUE
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# Codice di ottimizzazione REVENUE {#revenue-optimization-code}

Questa tabella fornisce informazioni dettagliate sulle notifiche di OTTIMIZZAZIONE DELLE ENTRATE.

## Abilita report di ottimizzazione ricavi {#enable-revenue-optimization-reporting}

Per abilitare questo rapporto, usa l’API PTMediaPlayer: `[mediaPlayer
setRevenueOptimizationReportingLevel:PTNotificationTypeInfo]`.

[!NNota]: La maggior parte delle notifiche informative contiene metadati rilevanti, ad esempio l’URL della risorsa che non è stato possibile scaricare. Alcune notifiche contengono metadati per specificare se il problema si è verificato nel contenuto video principale, nel contenuto audio alternativo o in un annuncio.

|Codice|Nome|Notifica interna|Tasti metadati|Commenti||—|—|—|—|—||401001| REVENUE_OPTIMIZATION_REPORTING| Nessuno| Consultare la tabella riportata di seguito per le chiavi di metadati basate su eventi diversi. | Nessuno|

| Dettagli evento | ContextMetadata |
|---|---|
| **CONTENT_RESOURCE_START** Inviato in TVSDK quando viene chiamato MediaPlayer::replaceCurrentResource. | clientTimestamp, fallbackOnInvalidCreative, showStaticBanners, hasPreroll, event, adSignalingMode, resourceUrl, creativeRepackageFormat, delayAdLoadingTolerance, zoneID, hasLivePreroll, adRequestTimeout, delayAdLoading, resourceType, creativeRepackageEnabled, mediaId, clientId |
| **CONTENT_PLAYBACK_START** Inviato in TVSDK quando il contenuto è entrato nello stato preparato ed è pronto per la riproduzione. Questo evento non verrà inviato su ogni caricamento del manifesto; verrà inviato solo sul caricamento iniziale. | clientTimestamp, contentURL, contentType, event, isLive, clientID |
| **AD_OPPORTUNITY_GENERATED** Inviato in TVSDK quando viene generata un&#39;opportunità. | clientTimestamp, evento, opportunitàId, placementDuration, clientId |
| **AD_OPPORTUNITY_RESOLVE_START** Inviato in TVSDK quando inizia la risoluzione di un&#39;opportunità. | clientTimestamp, evento, opportunitàId, placementDuration, clientId |
| **AD_OPPORTUNITY_RESOLVE_FAILED** Inviato in TVSDK quando un risolutore di annunci chiama MediaPlayerClient::notificationFailed(). Necessità di compilare i dati | opportunitàId, notificationAD |
| **AD_RESOURCE_LOAD** Inviato quando una risorsa annuncio viene recuperata dall&#39;URL. responseStartTime:marca temporale Unix per la prima volta che è iniziata la richiesta. responseTotalTime:quantità totale di tempo (in secondi) necessario per il caricamento di una risposta. responseStatus: il codice di stato rilevato durante il recupero della risorsa. status:&quot;error&quot; o &quot;success&quot; referrerAdId: l&#39;ID dell&#39;annuncio di provenienza che ha richiesto il recupero di questa risorsa (se presente). referrerUrl: l&#39;URL di provenienza del quale è stato richiesto il recupero della risorsa. errorMessage:Se lo stato è &quot;error&quot;, il motivo dell&#39;errore si trova qui. | experienceId, resourceType, responseTotalTime, responseStatus, responseStartTime, stato, errorMessage, url, referrerURL, referrerAdId |
| **AD_RESOURCE_LOAD_CRS** Inviato in TVSDK quando un CRS viene applicato a una risorsa, così come la risposta per m3u8. resourceType:always &quot;crs&quot;. responseStartTime:marca temporale Unix per la prima volta che è iniziata la richiesta. responseTotalTime:quantità totale di tempo (in secondi) necessario per il caricamento di una risposta. responseStatus: il codice di stato rilevato durante il recupero della risorsa. status:&quot;error&quot; o &quot;success&quot;. errorMessage:Se lo stato è &quot;error&quot;, il motivo dell&#39;errore si trova qui. mediaFileUrl:L&#39;URL del file multimediale originale selezionato. mediaFileBitrate:bitrate del file multimediale selezionato. mediaFileMimeType: Il tipo mime del file multimediale selezionato. url:L’URL della risorsa finale. | opportunitàId, resourceType, responseTotalTime, responseStatus, responseStartTime, stato, errorMessage, url, mediaFileURL, mediaFileBitrate, mediaFileMimeType, url |
| **AD_TIMELINE_PLACE** Inviato in TVSDK dopo che un adBreak è stato inserito nella timeline. Questo evento si verificherà una volta per ogni interruzione di annuncio. propostoTime: l&#39;ora in cui è stata richiesta l&#39;interruzione dell&#39;annuncio. effectiveTime: l’ora in cui l’interruzione dell’annuncio è stata effettivamente inserita. durataProposta: durata dell&#39;interruzione annuncio richiesta per l&#39;inserimento. Per il contenuto live questo è il periodo di tempo previsto. Per il contenuto VOD si tratterebbe normalmente di -1. effectiveDuration: la durata effettiva dell&#39;interruzione annuncio inserita. Calcolato come la durata della somma di tutti gli annunci, definita dalle rispettive durate del segmento, aggiunti o sostituiti nella timeline del flusso originale. proposteAnnunci: il numero di annunci nell&#39;interruzione annuncio proposta. totalAds: il numero di annunci inseriti correttamente. annunci pubblicitari...n:Gli annunci inseriti correttamente verranno inseriti qui. È possibile recuperare informazioni complete e manifesto da AD_OPPORTUNITY_RESOLVE_PROCESS | opportunitàId, stato, errorMessage, averageTime, proposteDuration, effectiveTime, effectiveDuration, proposteAds, totalAds, ads_id, ads_type, ads_Duration, ads_url |
| **AD_PLAYBACK_START** Inviato in TVSDK dopo l&#39;inizio della riproduzione di un annuncio. | clientTimestamp, evento, id, url, durata, tipo, opportunitàId, clientId |
| **AD_PLAYBACK_COMPLETE** Inviato in TVSDK dopo che un annuncio ha completato la riproduzione. | clientTimestamp, evento, id, url, durata, tipo, opportunitàId, clientId |
| **ADBREAK_PLAYBACK_START** Inviato in TVSDK quando viene avviata la riproduzione di un&#39;interruzione adbreak. | clientTimestamp, evento, entityId opportunità, durata, ora, clientId |
| **ADBREAK_PLAYBACK_COMPLETE** Inviato in TVSDK al termine della riproduzione di un&#39;interruzione adbreak. | clientTimestamp, evento, opportunitàId, clientId |
| **CONTENT_PLAYBACK_COMPLETE** Inviato in TVSDK quando viene completato un contenuto. Ciò potrebbe verificarsi se il flusso viene sostituito, il lettore immette uno stato di errore, il lettore viene reimpostato o il contenuto viene effettivamente completato. Questo evento sarà necessario per tenere traccia di sessionId. | clientTimestamp, evento, clientId, url, stato, errorMessage |
| **AD_PLAYBACK_ERROR** Inviato in TVSDK quando un annuncio presenta un errore durante la riproduzione (errori del flusso di variante). | evento, errore, timestamp, manifestUrl, ora, opportunitàId, url |