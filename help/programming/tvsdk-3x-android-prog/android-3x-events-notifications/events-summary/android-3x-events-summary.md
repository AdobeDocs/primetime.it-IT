---
description: L’applicazione può monitorare l’attività nel lettore e lo stato del lettore che cambia ascoltando gli eventi inviati da TVSDK.
title: Riepilogo eventi del lettore Primetime
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 0%

---


# Riepilogo eventi del lettore Primetime {#primetime-player-events-summary}

L’applicazione può monitorare l’attività nel lettore e lo stato del lettore che cambia ascoltando gli eventi inviati da TVSDK.

## Eventi {#events}

TVSDK notifica quando si verificano eventi a cui l’applicazione deve rispondere. Ogni evento corrisponde a una classe listener, con un metodo di callback che è necessario implementare.

>[!TIP]
>
>I codici evento sono le costanti dell&#39;enum `MediaPlayerEvent` .

`AdBreakCompletedEventListener`

* **** SignificatoLa riproduzione dell’interruzione annuncio è completa.

* **Callback per l’implementazione** `onAdBreakCompleted(AdBreakPlaybackEvent event)`

* **Codice evento** `AD_BREAK_COMPLETE`

`AdBreakSkippedEventListener`

* **** SignificatoUn&#39;interruzione annuncio è stata ignorata durante la riproduzione.

* **Callback per l’implementazione** `onAdBreakSkipped(AdBreakPlaybackEvent event)`

* **Codice evento** `AD_BREAK_SKIPPED`

`AdBreakStartedEventListener`

* **** SignificatoLa riproduzione dell’interruzione annuncio è iniziata.

* **Callback per l’implementazione** `onAdBreakStarted(AdBreakPlaybackEvent event)`

* **Codice evento** `AD_BREAK_START`

`AdClickedEventListener`

* **** SignificatoÈ stato fatto clic su un annuncio durante la riproduzione.

* **Callback per l’implementazione** `onAdClicked(AdClickEvent event)`
* **Codice evento** `AD_CLICK`

`AdCompletedEventListener`

* **** SignificatoLa riproduzione dell’annuncio è completa.

* **Callback per l’implementazione** `onAdCompleted(AdPlaybackEvent event)`

* **Codice evento** `AD_COMPLETE`

`AdProgressEventListener`

* **** SignificatoStato del reporting durante la riproduzione.

* **Callback per l’implementazione** `onAdProgress(AdPlaybackEvent event)`

* **Codice evento** `AD_PROGRESS`

`AdResolutionCompleteEventListener`

* **** Significato: risoluzione completa degli annunci Primetime. Questo evento è applicabile solo al contenuto VOD.

* **Callback per l’implementazione** `onAdResolutionComplete()`

* **Codice evento** `AD_RESOLUTION_COMPLETE`

`AdStartedEventListener`{#section_A4339C48F82640A8AF4AF09CB3B33188}

* **** SignificatoLa riproduzione dell’annuncio è iniziata.

* **Callback per l’implementazione** `onAdStarted(AdPlaybackEvent event)`

* **Codice evento** `AD_START`

`AudioUpdatedEventListener`

* **** SignificatoÈ stata rilevata una nuova traccia audio.

* **Callback per l’implementazione** `onAudioUpdated(MediaPlayerItemEvent event)`

* **Codice evento** `AUDIO_TRACK_UPDATED`

`BufferingBeginEventListener`

* **** SignificatoIl lettore ha iniziato il buffering.

* **Callback per l’implementazione** `onBufferingBegin(BufferEvent event)`

* **Codice evento** `BUFFERING_BEGIN`

`BufferingEndEventListener`

* **** SignificatoIl lettore ha interrotto il buffering.

* **Callback per l’implementazione** `onBufferingEnd(BufferEvent event)`

* **Codice evento** `BUFFERING_END`

`BufferPreparedEventListener&#39;

* **** SignificatoIl buffer è preparato.

* **Callback per l’implementazione** `onBufferPrepared()`

* **Codice evento** `BUFFER_PREPARED`

`CaptionsUpdatedEventListener`

* **** SignificatoÈ stata rilevata una nuova traccia della didascalia.

* **Callback per l’implementazione** `onCaptionsUpdated(MediaPlayerItemEvent event)`

* **Codice evento** `CAPTIONS_UPDATED`

`DRMMetadataInfoEventListener`

* **** SignificatoSono stati rilevati nuovi metadati DRM nel flusso multimediale.

* **Callback per l’implementazione** `onDRMMetadataInfo(DRMMetadataInfoEvent event)`

* **Codice evento** `DRM_METADATA`

`ItemCreatedEventListener`

* **** SignificatoÈ stato creato un nuovo elemento del lettore multimediale.

* **Callback per l’implementazione** `onItemCreated(MediaPlayerItemEvent event)`

* **Codice evento** `ITEM_CREATED`

`ItemLoadCompleteEventListener`

* **** Significato: sono state create nuove informazioni di caricamento per l’elemento corrente.

* **Callback per l’implementazione** `onLoadComplete(MediaPlayerItemEvent event)`

* **Codice evento** `ITEM_UPDATED`

`LoadInformationEventListener`

* **** SignificatoÈ stato caricato un nuovo segmento.

* **Callback per l’implementazione** `onLoadInformation(LoadInformationEvent event)`

* **Codice evento** `LOAD_INFORMATION_AVAILABLE`

`MainManifestUpdatedEventListener`

* **** SignificatoIl manifesto principale o la playlist è stata aggiornata.

* **Callback per l’implementazione** `onMainManifestUpdated(MediaPlayerItemEvent event)`

* **Codice evento** `MANIFEST_UPDATED`

`NotificationEventListener`

* **** SignificatoOperazione non riuscita.

* **Callback per l’implementazione** `onNotification(NotificationEvent event)`

* **Codice evento** `OPERATION_FAILED`

`PlaybackRangeUpdatedEventListener`

* **** SignificatoL’intervallo di riproduzione è stato aggiornato.

* **Callback per l’implementazione** `onPlaybackRangeUpdated(MediaPlayerItemEvent event)`

* **Codice evento** `PLAYBACK_RANGE_UPDATED`

`PlaybackRatePlayingEventListener`

* **** SignificatoUna nuova velocità di riproduzione è visibile sullo schermo.

* **Callback per l’implementazione** `onRatePlaying(PlaybackRateEvent event)`

* **Codice evento** `RATE_PLAYING`

`PlaybackRateSelectedEventListener`

* **** SignaningL&#39;attributo rate di MediaPlayer è stato impostato.

* **Callback per l’implementazione** `onRateSelected(PlaybackRateEvent event)`

* **Codice evento** `RATE_SELECTED`

`PlayStartEventListener`

* **** SignificatoLa riproduzione è iniziata.

* **Callback per l’implementazione** `onPlayStart()`

* **Codice evento** `PLAY_START`

`ProfileChangeEventListener`

* **** SignificatoIl profilo corrente di MediaPlayer è stato modificato.

* **Callback per l’implementazione** `onProfileChanged(ProfileEvent event)`

* **Codice evento** `PROFILE_CHANGED`

`ReservationReachedEventListener`

* **** SignaningPlayback ha raggiunto una prenotazione della timeline.

* **Callback per l’implementazione** `onReservationReached(ReservationEvent event)`

* **Codice evento** `RESERVATION_REACHED`

`SeekBeginEventListener`

* **** Operazione MeaningSeek avviata.

* **Callback per l’implementazione** `onSeekBegin(SeekEvent event)`

* **Codice evento** `SEEK_BEGIN`

`SeekEndEventListener`

* **** SignificatoOperazione di ricerca completata.

* **Callback per l’implementazione** `onSeekEnd(SeekEvent event)`

* **Codice evento** `SEEK_END`

`SeekPositionAdjustedEventListener`

* **** SignificatoLa posizione di ricerca è stata regolata a causa di regole di riproduzione interne o di regole di business esterne.

* **Callback per l’implementazione** `onPositionAdjusted(SeekEvent event)`

* **Codice evento** `SEEK_POSITION_ADJUSTED`

`SizeAvailableEventListener`

* **** SignificatoLe dimensioni del supporto sono disponibili.

* **Callback per l’implementazione** `onSizeAvailable(SizeAvailableEvent event)`

* **Codice evento** `SIZE_AVAILABLE`

`StatusChangeEventListener`

* **** SignificatoLo stato di MediaPlayer è stato modificato.

* **Callback per l’implementazione** `onStatusChanged(MediaPlayerStatusChangeEvent event)`

* **Codice evento** `STATUS_CHANGED`

`TimeChangeEventListener`

* **** SignificatoLa testina di riproduzione è cambiata.

* **Callback per l’implementazione** `onTimeChanged(TimeChangeEvent event)`

* **Codice evento** `TIME_CHANGED`

`TimedEventEventListener`

* **** SignificatoL’operazione è completa del tempo impiegato per l’operazione.

* **Callback per l’implementazione** `onTimedEvent(TimedEventEvent event)`

* **Codice evento** `TIMED_EVENT`

`TimelineMetadataAddedInBackgroundEventListener`

* **** SignificatoSono stati aggiunti nuovi metadati temporizzati a un elemento in background.

* **Callback per l’implementazione** `onTimedMetadata(TimedMetadataEvent event)`

* **Codice evento** `TIMED_METADATA_ADDED_IN_BACKGROUND`

`TimedMetadataEventListener`

* **** SignificatoNel flusso multimediale è stato rilevato un nuovo metadati temporizzati.

* **Callback per l’implementazione** `onTimedMetadata(TimedMetadataEvent event)`

* **Codice evento** `TIMED_METADATA_AVAILABLE`

`TimelineUpdatedEventListener`

* **** SignificatoLa timeline è stata modificata. Gli annunci potrebbero essere stati aggiunti o rimossi dalla timeline.

* **Callback per l’implementazione** `onTimelineUpdated(TimelineEvent event)`

* **Codice evento** `TIMELINE_UPDATED`