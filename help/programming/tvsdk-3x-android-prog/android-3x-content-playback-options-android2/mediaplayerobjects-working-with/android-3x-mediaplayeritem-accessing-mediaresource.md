---
description: I metodi della classe MediaPlayerItem consentono di ottenere informazioni sul flusso di contenuto rappresentato da un oggetto MediaResource caricato.
title: Metodi MediaPlayerItem per accedere alle informazioni MediaResource
exl-id: d6a547f3-0267-4a49-93a4-628b4879aef4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 0%

---

# Metodi MediaPlayerItem per accedere alle informazioni MediaResource {#mediaplayeritem-methods-for-accessing-mediaresource-information}

I metodi della classe MediaPlayerItem consentono di ottenere informazioni sul flusso di contenuto rappresentato da un oggetto MediaResource caricato.

| Metodo | Descrizione |
|--- |--- |
| **Tag annuncio** |  |
| Elenco`<String>` getAdTags() | Fornisce l’elenco dei tag di annunci utilizzati per il processo di posizionamento degli annunci. |
| **Streaming live** |  |
| booleano isLive(); | True se il flusso è attivo; false se è VOD. |
| **DRM protetto** |  |
| booleano isProtected(); | True se il flusso è protetto da DRM. |
| Elenco`<DRMMetadataInfo>` getDRMMetadataInfos(); | Elenca tutti gli oggetti metadati DRM individuati nel manifesto. |
| **Sottotitoli** |  |
| valore booleano hasClosedCaptions(); | True se sono disponibili tracce di sottotitoli. |
| Elenco`<ClosedCaptionsTrack>` getClosedCationsTracks(); | Fornisce un elenco delle tracce di sottotitoli. |
| ClosedCaptionsTrack ottiene SelectedClosedCaptionsTrack(); | Recupera il brano sottotitoli selezionato con SelectClosedCaptionsTrack. |
| selectClosedCaptionsTrack ( ClosedCaptionsTrack closedCaptionsTrack) | Imposta una traccia sottotitoli come traccia sottotitoli corrente. |
| **Tracce audio alternative** |  |
| booleano hasAlternateAudio(); | True se il flusso ha tracce audio alternative. Nota: anche la traccia audio principale (predefinita) fa parte dell&#39;elenco delle tracce audio alternative.  TVSDK per Android considera la traccia audio principale come una delle voci dell&#39;elenco delle tracce audio alternative. Per questo motivo, l&#39;unico caso in cui MediaPlayerItem.hasAlternateAudio restituisce false è quando il flusso non dispone di audio. Se il contenuto ha una sola traccia audio, questo metodo restituisce true e  `MediaPlayerItem.getAudioTracks`  restituisce un elenco con un singolo elemento (la traccia audio predefinita). |
| Elenco`<AudioTrack>` getAudioTracks(); | Fornisce un elenco delle tracce audio alternative disponibili. |
| AudioTrack getSelectedAudioTrack(); | Recupera la traccia audio selezionata con selectAudioTrack. |
| selectAudioTrack ( AudioTrack audio ) | Seleziona una traccia audio come traccia audio corrente. |
| **Metadati temporizzati** |  |
| hasTimedMetadata() booleano; | True se al flusso sono associati metadati temporizzati. |
| Elenco`<TimedMetadata>` getTimedMetadata(); | Fornisce un elenco degli oggetti metadati temporizzati associati al flusso. |
| **Profili multipli (velocità bit)** |
| booleano isDynamic(); | True se il flusso è un flusso MBR (Multiple Bit Rate). |
| Elenco`<Profile>` getProfiles(); | Fornisce un elenco dei profili di velocità bit associati. Per ogni profilo, puoi recuperarne la velocità in bit e l’altezza e la larghezza. |
| Profilo getSelectedProfile() | Recupera il profilo attualmente selezionato. |
| **Trick play** |  |
| valore booleano isTrickPlaySupported(); | True se il lettore supporta l&#39;avanzamento rapido, il riavvolgimento e la ripresa. |
| Elenco`< Float>` getAvailablePlaybackRates() | Fornisce l&#39;elenco delle velocità di riproduzione disponibili nel contesto della funzione di riproduzione con trick. |
| Float getSelectedPlaybackRate() | Recupera la velocità di riproduzione attualmente selezionata. |
| MediaPlayerItemConfig getConfig() | Restituisce l&#39;istanza MediaPlayerItemConfig associata a questo elemento. |
| **Risorsa multimediale** |  |
| MediaResource getResource(); | Restituisce la risorsa multimediale associata a questo elemento. |
| int getResourceId() | Restituisce l&#39;identificatore multimediale associato all&#39;elemento. Questo ID viene impostato quando l&#39;elemento viene caricato utilizzando MediaPlayerItemLoader.load . |
