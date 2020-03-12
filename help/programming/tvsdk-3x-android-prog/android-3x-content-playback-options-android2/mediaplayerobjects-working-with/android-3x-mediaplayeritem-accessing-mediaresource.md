---
description: I metodi della classe MediaPlayerItem consentono di ottenere informazioni sul flusso di contenuto rappresentato da un oggetto MediaResource caricato.
seo-description: I metodi della classe MediaPlayerItem consentono di ottenere informazioni sul flusso di contenuto rappresentato da un oggetto MediaResource caricato.
seo-title: Metodi MediaPlayerItem per accedere alle informazioni MediaResource
title: Metodi MediaPlayerItem per accedere alle informazioni MediaResource
uuid: 46845583-0a76-4411-a8bc-0a16ebfe8e6e
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Metodi MediaPlayerItem per accedere alle informazioni MediaResource {#mediaplayeritem-methods-for-accessing-mediaresource-information}

I metodi della classe MediaPlayerItem consentono di ottenere informazioni sul flusso di contenuto rappresentato da un oggetto MediaResource caricato.

| Metodo | Descrizione |
|--- |--- |
| **Tag ad** |  |
| List`<String>` getAdTags() | Fornisce l&#39;elenco dei tag degli annunci utilizzati per il processo di posizionamento degli annunci. |
| **Flusso live** |  |
| boolean isLive(); | True se il flusso è attivo; false se è VOD. |
| **Protezione DRM** |  |
| boolean isProtected(); | True se il flusso è protetto da DRM. |
| List`<DRMMetadataInfo>` getDRMMetadataInfos(); | Elenca tutti gli oggetti metadati DRM rilevati nel manifest. |
| **Sottotitoli codificati** |  |
| boolean hasClosedCaptions(); | True se sono disponibili tracce di sottotitoli codificati. |
| List`<ClosedCaptionsTrack>` getClosedCationsTracks(); | Fornisce un elenco delle tracce di sottotitoli codificati disponibili. |
| ClosedCaptionsTrack get SelectedClosedCaptionsTrack(); | Recupera la traccia dei sottotitoli codificati corrente selezionata con SelectClosedCaptionsTrack . |
| selectClosedCaptionsTrack ( ClosedCaptionsTrack closedCaptionsTrack ) | Imposta una traccia con didascalie chiuse come traccia corrente per i sottotitoli codificati. |
| **Tracce audio alternative** |  |
| boolean hasAlternateAudio(); | True se il flusso dispone di tracce audio alternative. Nota:  La traccia audio principale (predefinita) fa parte dell’elenco di tracce audio alternative.  TVSDK per Android considera la traccia audio principale come uno degli elementi nell’elenco delle tracce audio alternative. Per questo motivo, l’unico caso in cui MediaPlayerItem.hasAlternateAudio restituisce false è quando il flusso non ha alcun audio. Se il contenuto dispone di una sola traccia audio, questo metodo restituisce true e `MediaPlayerItem.getAudioTracks` restituisce un elenco con un singolo elemento (la traccia audio predefinita). |
| List`<AudioTrack>` getAudioTracks(); | Fornisce un elenco delle tracce audio alternative disponibili. |
| AudioTrack getSelectedAudioTrack(); | Recupera la traccia audio selezionata con selectAudioTrack . |
| selectAudioTrack ( AudioTrack audioTrack ) | Seleziona una traccia audio come traccia audio corrente. |
| **Metadati temporizzati** |  |
| boolean hasTimedMetadata(); | True se il flusso ha associato metadati temporizzati. |
| List`<TimedMetadata>` getTimedMetadata(); | Fornisce un elenco degli oggetti metadati temporizzati associati al flusso. |
| **Profili multipli (bitrate)** |
| boolean isDynamic(); | True se il flusso è un flusso MBR (bit rate multiplo). |
| List`<Profile>` getProfiles(); | Fornisce un elenco dei profili di bitrate associati. Per ciascun profilo, potete recuperarne il bitrate e l’altezza e la larghezza del profilo. |
| Profile getSelectedProfile() | Recupera il profilo attualmente selezionato. |
| **Gioco di mattoni** |  |
| boolean isTrickPlaySupported(); | True se il lettore supporta avanzamento rapido, riavvolgimento e ripresa. |
| List`< Float>` getAvailablePlaybackRates() | Fornisce l&#39;elenco delle frequenze di riproduzione disponibili nel contesto della funzione &quot;trucco-play&quot;. |
| Mobile getSelectedPlaybackRate() | Recupera la frequenza di riproduzione correntemente selezionata. |
| MediaPlayerItemConfig getConfig() | Restituisce l’istanza di MediaPlayerItemConfig associata a questo elemento. |
| **Risorse multimediali** |  |
| MediaResource getResource(); | Restituisce la risorsa multimediale associata all&#39;elemento. |
| int getResourceId() | Restituisce l&#39;identificatore multimediale associato all&#39;elemento. Questo ID viene impostato quando l’elemento viene caricato utilizzando MediaPlayerItemLoader.load. |