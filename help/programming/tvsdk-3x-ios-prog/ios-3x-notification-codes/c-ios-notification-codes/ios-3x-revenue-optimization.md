---
description: Questa tabella fornisce informazioni dettagliate sulle notifiche di ottimizzazione dei ricavi.
title: Codice ottimizzazione RICAVI
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 0%

---

# Codice ottimizzazione RICAVI {#revenue-optimization-code}

Questa tabella fornisce informazioni dettagliate sulle notifiche di OTTIMIZZAZIONE RICAVI.

## Abilita report di ottimizzazione dei ricavi {#enable-revenue-optimization-reporting}

Per abilitare questo reporting, utilizza l’api PTMediaPlayer: `[mediaPlayersetRevenueOptimizationReportingLevel:PTNotificationTypeInfo]`.

>[!NOTE]
>
>La maggior parte delle notifiche informative contiene metadati rilevanti, ad esempio l’URL della risorsa che non è stata scaricata. Alcune notifiche contengono metadati che consentono di specificare se il problema si è verificato nel contenuto video principale, nel contenuto audio alternativo o in un annuncio.

| Codice | Nome | Notifica interna | Chiavi metadati | Commenti |
|---|---|---|---|---|
| 401001 | REVENUE_OPTIMIZATION_REPORTING | Nessuno | Fai riferimento alla tabella seguente per le chiavi dei metadati basate su eventi diversi. | Nessuno |

| Dettagli evento | ContextMetadata |
|---|---|
| **CONTENT_RESOURCE_START** Inviato in TVSDK quando viene chiamato MediaPlayer::replaceCurrentResource. | clientTimestamp, fallbackOnInvalidCreative, showStaticBanners, hasPreroll, event, adSignalingMode, resourceUrl, creativeRepackagingFormat, delayAdLoadingTolerance, zoneID, hasLivePreroll, adRequestTimeout, delayAdLoading, resourceType, creativeRepackagingEnabled, mediaId, clientId |
| **CONTENT_PLAYBACK_START** Inviato in TVSDK quando il contenuto è entrato nello stato preparato ed è pronto per la riproduzione. Questo evento non viene inviato per ogni caricamento del manifesto, ma solo per il caricamento iniziale. | clientTimestamp, contentURL, contentType, event, isLive, clientID |
| **AD_OPPORTUNITY_GENERATED** Inviato in TVSDK quando viene generata un’opportunità. | clientTimestamp, evento, optionId, placementDuration, clientId |
| **AD_OPPORTUNITY_RESOLVE_START** Inviato in TVSDK quando inizia la risoluzione di un’opportunità. | clientTimestamp, evento, optionId, placementDuration, clientId |
| **AD_OPPORTUNITY_RESOLVE_FAILED** Inviato in TVSDK quando un ad resolver chiama MediaPlayerClient::notificationFailed(). È necessario compilare i dati | optionId, notificationAD |
| **AD_RESOURCE_LOAD** Inviato quando una risorsa annuncio viene recuperata dall’URL. responseStartTime:Timestamp Unix per il momento in cui è iniziata la richiesta. responseTotalTime: quantità totale di tempo (in secondi) necessaria per caricare una risposta. responseStatus: codice di stato rilevato durante il recupero della risorsa. stato: &quot;error&quot; o &quot;success&quot; referrerAdId: ID dell’annuncio di riferimento che ha richiesto il recupero di questa risorsa (se presente). referrerUrl: URL di riferimento che ha richiesto il recupero della risorsa. errorMessage:se lo stato è &quot;error&quot;, il motivo dell’errore si troverà qui. | optionId, resourceType, responseTotalTime, responseStatus, responseStartTime, status, errorMessage, url, referrerURL, referrerAdId |
| **AD_RESOURCE_LOAD_CRS** Inviato in TVSDK quando un CRS viene applicato a una risorsa, nonché la risposta per m3u8. resourceType:sempre &quot;crs&quot;. responseStartTime:Timestamp Unix per il momento in cui è iniziata la richiesta. responseTotalTime: quantità totale di tempo (in secondi) necessaria per caricare una risposta. responseStatus: codice di stato rilevato durante il recupero della risorsa. stato: &quot;error&quot; o &quot;success&quot;. errorMessage:se lo stato è &quot;error&quot;, il motivo dell’errore si troverà qui. mediaFileUrl:URL originale del file multimediale selezionato. mediaFileBitrate: il bitrate del file multimediale selezionato. mediaFileMimeType: il tipo mime del file multimediale selezionato. url: URL della risorsa finale. | optionId, resourceType, responseTotalTime, responseStatus, responseStartTime, status, errorMessage, url, mediaFileURL, mediaFileBitrate, mediaFileMimeType, url |
| **AD_TIMELINE_PLACE** Inviato in TVSDK dopo che un adBreak è stato inserito nella timeline. Questo evento si verificherà una volta per ogni interruzione pubblicitaria. posedTime: ora in cui è stato richiesto l&#39;inserimento dell&#39;interruzione pubblicitaria. actualTime: ora in cui è stata effettivamente inserita l&#39;interruzione pubblicitaria. posedDuration: durata dell’interruzione pubblicitaria richiesta per l’inserimento. Per il contenuto live, questo sarebbe la durata del segnale. Per il contenuto VOD, questo sarebbe normalmente -1. actualDuration: durata effettiva dell&#39;interruzione pubblicitaria inserita. Calcolata come la durata somma di tutti gli annunci, definita dalle rispettive durate del segmento, aggiunti o sostituiti nella timeline del flusso originale. annunci proposti:numero di annunci nell’interruzione pubblicitaria proposta. totalAds: numero di annunci inseriti correttamente. annunci...n:Gli annunci inseriti correttamente verranno inseriti qui. È possibile recuperare informazioni complete sul manifesto dell&#39;annuncio da AD_OPPORTUNITY_RESOLVE_PROCESS | NomeOpportunità, stato, messaggioErrore, oraProposta, durataProposta, oraEffettiva, durataEffettiva, annunciProposti, totaleAnnunci, ID_annunci, tipo_annunci, durata_annunci, URL_annunci |
| **AD_PLAYBACK_START** Inviato in TVSDK dopo che un annuncio inizia la riproduzione. | clientTimestamp, evento, id, url, durata, tipo, optionId, clientId |
| **AD_PLAYBACK_COMPLETE** Inviato in TVSDK dopo che la riproduzione di un annuncio è stata completata. | clientTimestamp, evento, id, url, durata, tipo, optionId, clientId |
| **ADBREAK_PLAYBACK_START** Inviato in TVSDK quando un’interruzione avvia la riproduzione. | clientTimestamp, evento, optionId, durata, ora, clientId |
| **ADBREAK_PLAYBACK_COMPLETE** Inviato in TVSDK quando un’interruzione pubblicitaria completa la riproduzione. | clientTimestamp, evento, optionId, clientId |
| **CONTENT_PLAYBACK_COMPLETE** Inviato in TVSDK quando viene completato qualsiasi contenuto. Ciò potrebbe verificarsi se il flusso viene sostituito, il lettore immette uno stato di errore, il lettore viene reimpostato o il contenuto viene effettivamente completato. Questo evento sarà necessario per tenere traccia di un sessionId. | clientTimestamp, event, clientId, url, status, errorMessage |
| **AD_PLAYBACK_ERROR** Inviato in TVSDK quando un annuncio presenta un errore di riproduzione (errori di flusso delle varianti). | event, error, Timestamp, manifestUrl, time, optionId, url |
