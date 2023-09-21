---
description: L’applicazione può monitorare l’attività nel lettore e il cambiamento dello stato del lettore ascoltando gli eventi inviati da TVSDK.
title: Riepilogo eventi del lettore Primetime
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# Riepilogo eventi del lettore Primetime {#primetime-player-events-summary}

L’applicazione può monitorare l’attività nel lettore e il cambiamento dello stato del lettore ascoltando gli eventi inviati da TVSDK.

## Eventi {#events}

TVSDK notifica quando si verificano eventi ai quali l&#39;applicazione deve rispondere. Ogni evento corrisponde a una classe listener, con un metodo di callback che è necessario implementare.

>[!TIP]
>
>I codici evento sono le costanti del `MediaPlayerEvent` enum.

`AdBreakCompletedEventListener`

* **Significato** Riproduzione dell’interruzione pubblicitaria completata.

* **Callback per implementare** `onAdBreakCompleted(AdBreakPlaybackEvent event)`

* **Codice evento** `AD_BREAK_COMPLETE`

`AdBreakSkippedEventListener`

* **Significato** Un’interruzione pubblicitaria è stata saltata durante la riproduzione.

* **Callback per implementare** `onAdBreakSkipped(AdBreakPlaybackEvent event)`

* **Codice evento** `AD_BREAK_SKIPPED`

`AdBreakStartedEventListener`

* **Significato** La riproduzione dell’interruzione pubblicitaria è stata avviata.

* **Callback per implementare** `onAdBreakStarted(AdBreakPlaybackEvent event)`

* **Codice evento** `AD_BREAK_START`

`AdClickedEventListener`

* **Significato** È stato fatto clic su un annuncio durante la riproduzione.

* **Callback per implementare** `onAdClicked(AdClickEvent event)`
* **Codice evento** `AD_CLICK`

`AdCompletedEventListener`

* **Significato** Riproduzione dell’annuncio completata.

* **Callback per implementare** `onAdCompleted(AdPlaybackEvent event)`

* **Codice evento** `AD_COMPLETE`

`AdProgressEventListener`

* **Significato** Avanzamento del reporting durante la riproduzione.

* **Callback per implementare** `onAdProgress(AdPlaybackEvent event)`

* **Codice evento** `AD_PROGRESS`

`AdResolutionCompleteEventListener`

* **Significato** La risoluzione dell’annuncio di Primetime ad decisioningè completa. Questo evento è applicabile solo al contenuto VOD.

* **Callback per implementare** `onAdResolutionComplete()`

* **Codice evento** `AD_RESOLUTION_COMPLETE`

`AdStartedEventListener`{#section_A4339C48F82640A8AF4AF09CB3B33188}

* **Significato** La riproduzione dell’annuncio è stata avviata.

* **Callback per implementare** `onAdStarted(AdPlaybackEvent event)`

* **Codice evento** `AD_START`

`AudioUpdatedEventListener`

* **Significato** È stata rilevata una nuova traccia audio.

* **Callback per implementare** `onAudioUpdated(MediaPlayerItemEvent event)`

* **Codice evento** `AUDIO_TRACK_UPDATED`

`BufferingBeginEventListener`

* **Significato** Il lettore ha iniziato il buffering.

* **Callback per implementare** `onBufferingBegin(BufferEvent event)`

* **Codice evento** `BUFFERING_BEGIN`

`BufferingEndEventListener`

* **Significato** Il lettore ha interrotto il buffering.

* **Callback per implementare** `onBufferingEnd(BufferEvent event)`

* **Codice evento** `BUFFERING_END`

`BufferPreparedEventListener`

* **Significato** Preparazione del buffer.

* **Callback per implementare** `onBufferPrepared()`

* **Codice evento** `BUFFER_PREPARED`

`CaptionsUpdatedEventListener`

* **Significato** È stata rilevata una nuova traccia di didascalia.

* **Callback per implementare** `onCaptionsUpdated(MediaPlayerItemEvent event)`

* **Codice evento** `CAPTIONS_UPDATED`

`DRMMetadataInfoEventListener`

* **Significato** Nel flusso multimediale è stato rilevato un nuovo metadati DRM.

* **Callback per implementare** `onDRMMetadataInfo(DRMMetadataInfoEvent event)`

* **Codice evento** `DRM_METADATA`

`ItemCreatedEventListener`

* **Significato** È stato creato un nuovo elemento del lettore multimediale.

* **Callback per implementare** `onItemCreated(MediaPlayerItemEvent event)`

* **Codice evento** `ITEM_CREATED`

`ItemLoadCompleteEventListener`

* **Significato** Sono state create nuove informazioni di caricamento per l&#39;elemento corrente.

* **Callback per implementare** `onLoadComplete(MediaPlayerItemEvent event)`

* **Codice evento** `ITEM_UPDATED`

`LoadInformationEventListener`

* **Significato** È stato caricato un nuovo segmento.

* **Callback per implementare** `onLoadInformation(LoadInformationEvent event)`

* **Codice evento** `LOAD_INFORMATION_AVAILABLE`

`MainManifestUpdatedEventListener`

* **Significato** Il manifesto principale o la playlist è stata aggiornata.

* **Callback per implementare** `onMainManifestUpdated(MediaPlayerItemEvent event)`

* **Codice evento** `MANIFEST_UPDATED`

`NotificationEventListener`

* **Significato** Operazione non riuscita.

* **Callback per implementare** `onNotification(NotificationEvent event)`

* **Codice evento** `OPERATION_FAILED`

`PlaybackRangeUpdatedEventListener`

* **Significato** L’intervallo di riproduzione è stato aggiornato.

* **Callback per implementare** `onPlaybackRangeUpdated(MediaPlayerItemEvent event)`

* **Codice evento** `PLAYBACK_RANGE_UPDATED`

`PlaybackRatePlayingEventListener`

* **Significato** Sullo schermo è visibile una nuova velocità di riproduzione.

* **Callback per implementare** `onRatePlaying(PlaybackRateEvent event)`

* **Codice evento** `RATE_PLAYING`

`PlaybackRateSelectedEventListener`

* **Significato** L&#39;attributo rate di MediaPlayer è stato impostato.

* **Callback per implementare** `onRateSelected(PlaybackRateEvent event)`

* **Codice evento** `RATE_SELECTED`

`PlayStartEventListener`

* **Significato** Riproduzione avviata.

* **Callback per implementare** `onPlayStart()`

* **Codice evento** `PLAY_START`

`ProfileChangeEventListener`

* **Significato** Il profilo corrente di MediaPlayer è stato modificato.

* **Callback per implementare** `onProfileChanged(ProfileEvent event)`

* **Codice evento** `PROFILE_CHANGED`

`ReservationReachedEventListener`

* **Significato** La riproduzione ha raggiunto una prenotazione della timeline.

* **Callback per implementare** `onReservationReached(ReservationEvent event)`

* **Codice evento** `RESERVATION_REACHED`

`SeekBeginEventListener`

* **Significato** Operazione di ricerca avviata.

* **Callback per implementare** `onSeekBegin(SeekEvent event)`

* **Codice evento** `SEEK_BEGIN`

`SeekEndEventListener`

* **Significato** Operazione di ricerca completata.

* **Callback per implementare** `onSeekEnd(SeekEvent event)`

* **Codice evento** `SEEK_END`

`SeekPositionAdjustedEventListener`

* **Significato** La posizione di ricerca è stata regolata a causa di regole di riproduzione interne o regole aziendali esterne.

* **Callback per implementare** `onPositionAdjusted(SeekEvent event)`

* **Codice evento** `SEEK_POSITION_ADJUSTED`

`SizeAvailableEventListener`

* **Significato** Dimensione del supporto disponibile.

* **Callback per implementare** `onSizeAvailable(SizeAvailableEvent event)`

* **Codice evento** `SIZE_AVAILABLE`

`StatusChangeEventListener`

* **Significato** Lo stato di MediaPlayer è cambiato.

* **Callback per implementare** `onStatusChanged(MediaPlayerStatusChangeEvent event)`

* **Codice evento** `STATUS_CHANGED`

`TimeChangeEventListener`

* **Significato** La testina di riproduzione è cambiata.

* **Callback per implementare** `onTimeChanged(TimeChangeEvent event)`

* **Codice evento** `TIME_CHANGED`

`TimedEventEventListener`

* **Significato** Operazione completata con il tempo necessario per l&#39;operazione.

* **Callback per implementare** `onTimedEvent(TimedEventEvent event)`

* **Codice evento** `TIMED_EVENT`

`TimelineMetadataAddedInBackgroundEventListener`

* **Significato** Sono stati aggiunti nuovi metadati temporizzati a un elemento in background.

* **Callback per implementare** `onTimedMetadata(TimedMetadataEvent event)`

* **Codice evento** `TIMED_METADATA_ADDED_IN_BACKGROUND`

`TimedMetadataEventListener`

* **Significato** Nel flusso multimediale è stato rilevato un nuovo metadati temporizzati.

* **Callback per implementare** `onTimedMetadata(TimedMetadataEvent event)`

* **Codice evento** `TIMED_METADATA_AVAILABLE`

`TimelineUpdatedEventListener`

* **Significato** La timeline è stata modificata. Gli annunci potrebbero essere stati aggiunti o rimossi dalla timeline.

* **Callback per implementare** `onTimelineUpdated(TimelineEvent event)`

* **Codice evento** `TIMELINE_UPDATED`
