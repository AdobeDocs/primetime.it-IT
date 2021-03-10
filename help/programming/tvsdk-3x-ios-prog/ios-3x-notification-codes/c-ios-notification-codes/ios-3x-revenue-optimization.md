---
description: 'Questa tabella fornisce informazioni dettagliate sulle notifiche di ottimizzazione dei ricavi. '
title: Codice di ottimizzazione dei ricavi
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 0%

---


# Codice di ottimizzazione dei ricavi {#revenue-optimization-code}

Questa tabella fornisce informazioni dettagliate sulle notifiche di OTTIMIZZAZIONE DEI RICAVI.

## Abilitare i rapporti di ottimizzazione dei ricavi {#enable-revenue-optimization-reporting}

Per abilitare questo reporting, utilizza l&#39;api PTMediaPlayer: `[mediaPlayersetRevenueOptimizationReportingLevel:PTNotificationTypeInfo]`.

>[!NOTE]
>
>La maggior parte delle notifiche informative contiene metadati rilevanti, ad esempio l’URL della risorsa che non è stato possibile scaricare. Alcune notifiche contengono metadati per specificare se il problema si è verificato nel contenuto video principale, nel contenuto audio alternativo o in un annuncio.

| Codice | Nome | Notifica interna | Chiavi metadati | Commenti |
|---|---|---|---|---|
| 401001 | REVENUE_OPTIMIZATION_REPORTING | Nessuno | Fai riferimento alla tabella seguente per le chiavi di metadati basate su eventi diversi. | Nessuno |

| Dettagli evento | ContextMetadata |
|---|---|
| **CONTENT_RESOURCE_** STARTDispatched in TVSDK quando viene chiamato MediaPlayer::replaceCurrentResource. | clientTimestamp, fallbackOnInvalidCreative, showStaticBanner, hasPreroll, event, adSignalingMode, resourceUrl, creativeRepackagingFormat, delayAdLoadingTolerance, zoneID, hasLivePreroll, adRequestTimeout, delayAdLoading, resourceType, creativeRepackagingEnabled, media clientId |
| **CONTENT_PLAYBACK_** STARTDispatched in TVSDK quando il contenuto è entrato nello stato preparato ed è pronto per la riproduzione. Questo evento non invierà su ogni caricamento del manifesto - invierà solo al caricamento iniziale. | clientTimestamp, contentURL, contentType, event, isLive, clientID |
| **AD_OPPORTUNITY_** GENERATEDDispatched in TVSDK quando viene generata un&#39;opportunità. | clientTimestamp, evento, entity, ileId, placementDuration, clientId |
| **AD_OPPORTUNITY_RESOLVE_** STARTDispatched in TVSDK quando viene avviata la risoluzione di un&#39;opportunità. | clientTimestamp, evento, entity, ileId, placementDuration, clientId |
| **AD_OPPORTUNITY_RESOLVE_** FAILEDDispatched in TVSDK quando un ad resolver chiama MediaPlayerClient::notifyFailed(). Necessità di compilare i dati | opportunitàId, notificationAD |
| **AD_RESOURCE_** LOADDispatched quando una qualsiasi risorsa di annunci viene recuperata dall&#39;URL. responseStartTime:Unix timestamp per l&#39;avvio della richiesta. responseTotalTime:quantità totale di tempo (in secondi) necessario per il caricamento di una risposta. responseStatus:Il codice di stato rilevato durante il recupero della risorsa. status:&quot;error&quot; o &quot;success&quot; referrerAdId:l&#39;id dell&#39;annuncio di riferimento che ha richiesto il recupero di questa risorsa (se presente). referrerUrl:URL di provenienza che ha richiesto il recupero di questa risorsa. errorMessage:Se lo stato è &quot;error&quot;, il motivo dell&#39;errore si trova qui. | opportunitàId, resourceType, responseTotalTime, responseStatus, responseStartTime, status, errorMessage, url, referrerURL, referrerAdId |
| **AD_RESOURCE_LOAD_** CRSDispatched in TVSDK quando un CRS viene applicato a una risorsa, così come la risposta per m3u8. resourceType:always &quot;crs&quot;. responseStartTime:Unix timestamp per l&#39;avvio della richiesta. responseTotalTime:quantità totale di tempo (in secondi) necessario per il caricamento di una risposta. responseStatus:Il codice di stato rilevato durante il recupero della risorsa. status:&quot;error&quot; o &quot;success&quot;. errorMessage:Se lo stato è &quot;error&quot;, il motivo dell&#39;errore si trova qui. mediaFileUrl:URL del file multimediale originale selezionato. mediaFileBitrate:Il bitrate del file multimediale selezionato. mediaFileMimeType: Il tipo MIME del file multimediale selezionato. url:url della risorsa finale. | opportunitàId, resourceType, responseTotalTime, responseStatus, responseStartTime, status, errorMessage, url, mediaFileURL, mediaFileBitrate, mediaFileMimeType, url |
| **AD_TIMELINE_** PLACEDispatched in TVSDK dopo che un adBreak è stato inserito sulla timeline. Questo evento si verifica una volta per ogni interruzione pubblicitaria. propostoTime:l’ora in cui è stata richiesta l’interruzione pubblicitaria. realTime:l’ora in cui l’interruzione pubblicitaria è stata effettivamente inserita. durataProposta:la durata dell&#39;interruzione pubblicitaria richiesta per l&#39;inserimento. Per i contenuti live questa è la durata del cue. Per il contenuto VOD si tratta normalmente di -1. effectiveDuration:la durata effettiva dell’interruzione pubblicitaria inserita. Calcolato come la durata della somma di tutti gli annunci, definita dalle rispettive durate del segmento, aggiunto o sostituito nella timeline del flusso originale. proposteAds:il numero di annunci nell’interruzione pubblicitaria proposta. totalAds:il numero di annunci inseriti correttamente. annunci pubblicitari...n:Gli annunci inseriti correttamente verranno inseriti qui. È possibile recuperare informazioni complete e manifeste da AD_OPPORTUNITY_RESOLVE_PROCESS | OpportunitàId, stato, errorMessage, offerTime, durataProposta, tempoEffettivo, DurataEffettiva, annunciProposti, annunciTotale, annunci_id, ads_type, ads_duration, ads_url |
| **AD_PLAYBACK_** STARTDispatched in TVSDK dopo l&#39;inizio della riproduzione di un annuncio. | clientTimestamp, evento, id, url, durata, tipo, petrolioSpedent, clientId |
| **AD_PLAYBACK_** COMPLETEDispatched in TVSDK dopo che un annuncio ha completato la riproduzione. | clientTimestamp, evento, id, url, durata, tipo, petrolioSpedent, clientId |
| **ADBREAK_PLAYBACK_** STARTDispatched in TVSDK quando un adbreak avvia la riproduzione. | clientTimestamp, evento, OpportunitàId, durata, ora, clientId |
| **ADBREAK_PLAYBACK_** COMPLETEDispatched in TVSDK quando una pausa completa la riproduzione. | clientTimestamp, evento, opportunitàId, clientId |
| **CONTENT_PLAYBACK_** COMPLETEDspeched in TVSDK quando viene completato un contenuto. Questo potrebbe verificarsi se il flusso viene sostituito, il lettore immette uno stato di errore, il lettore viene reimpostato o il contenuto viene effettivamente completato. Questo evento sarà necessario per tenere traccia di un sessionId. | clientTimestamp, evento, clientId, url, stato, errorMessage |
| **AD_PLAYBACK_** ERRORDinviato in TVSDK quando un annuncio presenta un errore di riproduzione (errori di flusso variante). | evento, errore, timestamp, manifestUrl, time, opportunitàId, url |
