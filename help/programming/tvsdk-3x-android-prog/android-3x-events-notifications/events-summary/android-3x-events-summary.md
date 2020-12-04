---
description: L’applicazione può monitorare l’attività nel lettore e lo stato di modifica del lettore ascoltando gli eventi inviati da TVSDK.
seo-description: L’applicazione può monitorare l’attività nel lettore e lo stato di modifica del lettore ascoltando gli eventi inviati da TVSDK.
seo-title: Riepilogo degli eventi del lettore Primetime
title: Riepilogo degli eventi del lettore Primetime
uuid: b2ff74f2-c373-42da-a717-2f0550cbcb7f
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 0%

---


# Riepilogo eventi del lettore Primetime {#primetime-player-events-summary}

L’applicazione può monitorare l’attività nel lettore e lo stato di modifica del lettore ascoltando gli eventi inviati da TVSDK.

## Eventi {#events}

TVSDK avvisa quando si verificano eventi ai quali l’applicazione deve rispondere. Ogni evento corrisponde a una classe listener, con un metodo di callback che è necessario implementare.

>[!TIP]
>
>I codici evento sono le costanti dell&#39;enum `MediaPlayerEvent`.

`AdBreakCompletedEventListener`

* **** Significato: la riproduzione dell’interruzione dell’annuncio è completa.

* **Callback per l&#39;implementazione** `onAdBreakCompleted(AdBreakPlaybackEvent event)`

* **Codice evento** `AD_BREAK_COMPLETE`

`AdBreakSkippedEventListener`

* **Significato:** durante la riproduzione è stata saltata un&#39;interruzione annuncio.

* **Callback per l&#39;implementazione** `onAdBreakSkipped(AdBreakPlaybackEvent event)`

* **Codice evento** `AD_BREAK_SKIPPED`

`AdBreakStartedEventListener`

* **Significato:** la riproduzione dell’interruzione annuncio è iniziata.

* **Callback per l&#39;implementazione** `onAdBreakStarted(AdBreakPlaybackEvent event)`

* **Codice evento** `AD_BREAK_START`

`AdClickedEventListener`

* **Significato:** durante la riproduzione è stato fatto clic su un annuncio.

* **Callback per l&#39;implementazione** `onAdClicked(AdClickEvent event)`
* **Codice evento** `AD_CLICK`

`AdCompletedEventListener`

* **** Significato: la riproduzione dell’annuncio è completa.

* **Callback per l&#39;implementazione** `onAdCompleted(AdPlaybackEvent event)`

* **Codice evento** `AD_COMPLETE`

`AdProgressEventListener`

* **Significato:** Segnalazione dell’avanzamento durante la riproduzione.

* **Callback per l&#39;implementazione** `onAdProgress(AdPlaybackEvent event)`

* **Codice evento** `AD_PROGRESS`

`AdResolutionCompleteEventListener`

* **Significato: risoluzione** annunci Primetime e risoluzione completa. Questo evento è applicabile solo al contenuto VOD.

* **Callback per l&#39;implementazione** `onAdResolutionComplete()`

* **Codice evento** `AD_RESOLUTION_COMPLETE`

`AdStartedEventListener`{#section_A4339C48F82640A8AF4AF09CB3B33188}

* **** Significato: la riproduzione dell’annuncio è iniziata.

* **Callback per l&#39;implementazione** `onAdStarted(AdPlaybackEvent event)`

* **Codice evento** `AD_START`

`AudioUpdatedEventListener`

* **** Significato: è stata rilevata una nuova traccia audio.

* **Callback per l&#39;implementazione** `onAudioUpdated(MediaPlayerItemEvent event)`

* **Codice evento** `AUDIO_TRACK_UPDATED`

`BufferingBeginEventListener`

* **** Significato: Il giocatore ha iniziato a bufferizzare.

* **Callback per l&#39;implementazione** `onBufferingBegin(BufferEvent event)`

* **Codice evento** `BUFFERING_BEGIN`

`BufferingEndEventListener`

* **** Significato: il lettore ha interrotto la bufferizzazione.

* **Callback per l&#39;implementazione** `onBufferingEnd(BufferEvent event)`

* **Codice evento** `BUFFERING_END`

&quot;BufferPreparedEventListener&quot;

* **Significato:** Il buffer è preparato.

* **Callback per l&#39;implementazione** `onBufferPrepared()`

* **Codice evento** `BUFFER_PREPARED`

`CaptionsUpdatedEventListener`

* **** Significato: è stata rilevata una nuova traccia di didascalia.

* **Callback per l&#39;implementazione** `onCaptionsUpdated(MediaPlayerItemEvent event)`

* **Codice evento** `CAPTIONS_UPDATED`

`DRMMetadataInfoEventListener`

* **** Significato: nel flusso multimediale è stato rilevato un nuovo metadati DRM.

* **Callback per l&#39;implementazione** `onDRMMetadataInfo(DRMMetadataInfoEvent event)`

* **Codice evento** `DRM_METADATA`

`ItemCreatedEventListener`

* **** Significato: è stato creato un nuovo elemento del lettore multimediale.

* **Callback per l&#39;implementazione** `onItemCreated(MediaPlayerItemEvent event)`

* **Codice evento** `ITEM_CREATED`

`ItemLoadCompleteEventListener`

* **** Significato: sono state create nuove informazioni sul caricamento per l’elemento corrente.

* **Callback per l&#39;implementazione** `onLoadComplete(MediaPlayerItemEvent event)`

* **Codice evento** `ITEM_UPDATED`

`LoadInformationEventListener`

* **** Significato: è stato caricato un nuovo segmento.

* **Callback per l&#39;implementazione** `onLoadInformation(LoadInformationEvent event)`

* **Codice evento** `LOAD_INFORMATION_AVAILABLE`

`MainManifestUpdatedEventListener`

* **** Significato: il manifesto o la playlist principale è stato aggiornato.

* **Callback per l&#39;implementazione** `onMainManifestUpdated(MediaPlayerItemEvent event)`

* **Codice evento** `MANIFEST_UPDATED`

`NotificationEventListener`

* **** Significato: operazione non riuscita.

* **Callback per l&#39;implementazione** `onNotification(NotificationEvent event)`

* **Codice evento** `OPERATION_FAILED`

`PlaybackRangeUpdatedEventListener`

* **** Significato: l’intervallo di riproduzione è stato aggiornato.

* **Callback per l&#39;implementazione** `onPlaybackRangeUpdated(MediaPlayerItemEvent event)`

* **Codice evento** `PLAYBACK_RANGE_UPDATED`

`PlaybackRatePlayingEventListener`

* **Significato:** sullo schermo è visibile una nuova frequenza di riproduzione.

* **Callback per l&#39;implementazione** `onRatePlaying(PlaybackRateEvent event)`

* **Codice evento** `RATE_PLAYING`

`PlaybackRateSelectedEventListener`

* **** Significato: l&#39;attributo rate di MediaPlayer è stato impostato.

* **Callback per l&#39;implementazione** `onRateSelected(PlaybackRateEvent event)`

* **Codice evento** `RATE_SELECTED`

`PlayStartEventListener`

* **Significato:** la riproduzione è iniziata.

* **Callback per l&#39;implementazione** `onPlayStart()`

* **Codice evento** `PLAY_START`

`ProfileChangeEventListener`

* **** Significato: il profilo corrente di MediaPlayer è cambiato.

* **Callback per l&#39;implementazione** `onProfileChanged(ProfileEvent event)`

* **Codice evento** `PROFILE_CHANGED`

`ReservationReachedEventListener`

* **** SignificatoRiproduzione ha raggiunto una prenotazione della timeline.

* **Callback per l&#39;implementazione** `onReservationReached(ReservationEvent event)`

* **Codice evento** `RESERVATION_REACHED`

`SeekBeginEventListener`

* **Operazione** MeaningSeek avviata.

* **Callback per l&#39;implementazione** `onSeekBegin(SeekEvent event)`

* **Codice evento** `SEEK_BEGIN`

`SeekEndEventListener`

* **** Significato: operazione di ricerca completata.

* **Callback per l&#39;implementazione** `onSeekEnd(SeekEvent event)`

* **Codice evento** `SEEK_END`

`SeekPositionAdjustedEventListener`

* **Significato:** la posizione di ricerca è stata regolata a causa di regole di riproduzione interne o regole aziendali esterne.

* **Callback per l&#39;implementazione** `onPositionAdjusted(SeekEvent event)`

* **Codice evento** `SEEK_POSITION_ADJUSTED`

`SizeAvailableEventListener`

* **** SignificatoLe dimensioni del supporto sono disponibili.

* **Callback per l&#39;implementazione** `onSizeAvailable(SizeAvailableEvent event)`

* **Codice evento** `SIZE_AVAILABLE`

`StatusChangeEventListener`

* **** Significato: lo stato di MediaPlayer è cambiato.

* **Callback per l&#39;implementazione** `onStatusChanged(MediaPlayerStatusChangeEvent event)`

* **Codice evento** `STATUS_CHANGED`

`TimeChangeEventListener`

* **Significato:** La testina di riproduzione è cambiata.

* **Callback per l&#39;implementazione** `onTimeChanged(TimeChangeEvent event)`

* **Codice evento** `TIME_CHANGED`

`TimedEventEventListener`

* **** SignificatoL&#39;operazione è completa con il tempo necessario per l&#39;operazione.

* **Callback per l&#39;implementazione** `onTimedEvent(TimedEventEvent event)`

* **Codice evento** `TIMED_EVENT`

`TimelineMetadataAddedInBackgroundEventListener`

* **** Significato: a un elemento in background sono stati aggiunti nuovi metadati temporizzati.

* **Callback per l&#39;implementazione** `onTimedMetadata(TimedMetadataEvent event)`

* **Codice evento** `TIMED_METADATA_ADDED_IN_BACKGROUND`

`TimedMetadataEventListener`

* **** Significato: nel flusso multimediale sono stati rilevati nuovi metadati temporizzati.

* **Callback per l&#39;implementazione** `onTimedMetadata(TimedMetadataEvent event)`

* **Codice evento** `TIMED_METADATA_AVAILABLE`

`TimelineUpdatedEventListener`

* **** Significato: la timeline è stata modificata. Gli annunci potrebbero essere stati aggiunti o rimossi dalla timeline.

* **Callback per l&#39;implementazione** `onTimelineUpdated(TimelineEvent event)`

* **Codice evento** `TIMELINE_UPDATED`