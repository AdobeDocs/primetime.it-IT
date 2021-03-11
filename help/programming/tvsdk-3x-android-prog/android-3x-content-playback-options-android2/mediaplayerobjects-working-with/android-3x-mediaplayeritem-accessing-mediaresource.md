---
description: I metodi della classe MediaPlayerItem ti consentono di ottenere informazioni sul flusso di contenuto rappresentato da un MediaResource caricato.
title: Metodi MediaPlayerItem per accedere alle informazioni di MediaResource
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 0%

---


# Metodi MediaPlayerItem per accedere alle informazioni di MediaResource {#mediaplayeritem-methods-for-accessing-mediaresource-information}

I metodi della classe MediaPlayerItem ti consentono di ottenere informazioni sul flusso di contenuto rappresentato da un MediaResource caricato.

| Metodo | Descrizione |
|--- |--- |
| **Tag annunci** |  |
| List`<String>` getAdTags() | Fornisce l&#39;elenco dei tag degli annunci utilizzati per il processo di posizionamento degli annunci. |
| **Flusso live** |  |
| booleano isLive(); | True se il flusso è attivo; false se è VOD. |
| **DRM protetto** |  |
| booleano isProtected(); | True se il flusso è protetto DRM. |
| List`<DRMMetadataInfo>` getDRMMetadataInfos(); | Elenca tutti gli oggetti metadati DRM scoperti nel manifesto. |
| **Sottotitoli codificati** |  |
| booleano hasClosedCaptions(); | True se sono disponibili tracce di sottotitoli. |
| List`<ClosedCaptionsTrack>` getClosedCationsTracks(); | Fornisce un elenco delle tracce di sottotitoli disponibili. |
| ClosedCaptionsTrack get SelectedClosedCaptionsTrack(); | Recupera la traccia corrente della didascalia chiusa selezionata con SelectClosedCaptionsTrack . |
| selectClosedCaptionsTrack ( ClosedCaptionsTrack closedCaptionsTrack) | Imposta una traccia a didascalia chiusa come traccia corrente a didascalia chiusa. |
| **Tracce audio alternative** |  |
| booleano hasAlternateAudio(); | True se il flusso dispone di tracce audio alternative. Nota:  La traccia audio principale (predefinita) fa anche parte dell’elenco di tracce audio alternative.  TVSDK per Android considera la traccia audio principale come uno degli elementi nell’elenco di tracce audio alternative. Per questo motivo, l&#39;unico caso in cui MediaPlayerItem.hasAlternateAudio restituisce false è quando il flusso non ha alcun audio. Se il contenuto dispone di una sola traccia audio, questo metodo restituisce true e `MediaPlayerItem.getAudioTracks` restituisce un elenco con un singolo elemento (la traccia audio predefinita). |
| List`<AudioTrack>` getAudioTracks(); | Fornisce un elenco delle tracce audio alternative disponibili. |
| AudioTrack getSelectedAudioTrack(); | Recupera la traccia audio selezionata con selectAudioTrack . |
| selectAudioTrack ( AudioTrack audioTrack ) | Seleziona una traccia audio come traccia audio corrente. |
| **Metadati temporizzati** |  |
| booleano hasTimedMetadata(); | True se il flusso ha associato metadati temporizzati. |
| List`<TimedMetadata>` getTimedMetadata(); | Fornisce un elenco degli oggetti metadati temporizzati associati al flusso. |
| **Profili multipli (bit rate)** |
| booleano isDynamic(); | True se il flusso è un flusso a bit rate multiplo (MBR). |
| List`<Profile>` getProfiles(); | Fornisce un elenco dei profili di bit rate associati. Per ciascun profilo, puoi recuperarne il bit rate e l’altezza e la larghezza del profilo. |
| Profilo getSelectedProfile() | Recupera il profilo attualmente selezionato. |
| **Gioco di mattoni** |  |
| isTrickPlaySupported() booleano; | True se il lettore supporta l&#39;avanzamento rapido, il riavvolgimento e la ripresa. |
| List`< Float>` getAvailablePlaybackRates() | Fornisce l&#39;elenco delle velocità di riproduzione disponibili nel contesto della funzione di riproduzione a forma di trucco. |
| Mobile getSelectedPlaybackRate() | Recupera la velocità di riproduzione attualmente selezionata. |
| MediaPlayerItemConfig getConfig() | Restituisce l&#39;istanza MediaPlayerItemConfig associata a questo elemento. |
| **Risorsa multimediale** |  |
| MediaResource getResource(); | Restituisce la risorsa multimediale associata all&#39;elemento. |
| int getResourceId() | Restituisce l&#39;identificatore multimediale associato all&#39;elemento. Questo ID viene impostato quando l&#39;elemento viene caricato utilizzando MediaPlayerItemLoader.load . |