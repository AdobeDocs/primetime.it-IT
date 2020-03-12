---
description: L’applicazione può monitorare l’attività nel lettore e lo stato di modifica del lettore ascoltando gli eventi inviati da TVSDK.
seo-description: L’applicazione può monitorare l’attività nel lettore e lo stato di modifica del lettore ascoltando gli eventi inviati da TVSDK.
seo-title: Riepilogo degli eventi del lettore Primetime
title: Riepilogo degli eventi del lettore Primetime
uuid: b2ff74f2-c373-42da-a717-2f0550cbcb7f
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Riepilogo degli eventi del lettore Primetime {#primetime-player-events-summary}

L’applicazione può monitorare l’attività nel lettore e lo stato di modifica del lettore ascoltando gli eventi inviati da TVSDK.

## Eventi {#events}

TVSDK avvisa quando si verificano eventi ai quali l’applicazione deve rispondere. Ogni evento corrisponde a una classe listener, con un metodo di callback che è necessario implementare.

>[!TIP]
>
>I codici evento sono le costanti dell&#39; `MediaPlayerEvent` enum.

`AdBreakCompletedEventListener`

* **Significato** La riproduzione dell&#39;interruzione dell&#39;annuncio è completa.

* **Callback per l&#39;implementazione**`onAdBreakCompleted(AdBreakPlaybackEvent event)`

* **Codice** evento `AD_BREAK_COMPLETE`

`AdBreakSkippedEventListener`

* **Significato** Un&#39;interruzione annuncio è stata saltata durante la riproduzione.

* **Callback per l&#39;implementazione**`onAdBreakSkipped(AdBreakPlaybackEvent event)`

* **Codice** evento `AD_BREAK_SKIPPED`

`AdBreakStartedEventListener`

* **Significato** La riproduzione dell&#39;interruzione annuncio è iniziata.

* **Callback per l&#39;implementazione**`onAdBreakStarted(AdBreakPlaybackEvent event)`

* **Codice** evento `AD_BREAK_START`

`AdClickedEventListener`

* **Significato** È stato fatto clic su un annuncio durante la riproduzione.

* **Callback per l&#39;implementazione**`onAdClicked(AdClickEvent event)`
* **Codice** evento `AD_CLICK`

`AdCompletedEventListener`

* **Significato** La riproduzione dell&#39;annuncio è completa.

* **Callback per l&#39;implementazione**`onAdCompleted(AdPlaybackEvent event)`

* **Codice** evento `AD_COMPLETE`

`AdProgressEventListener`

* **Significato** Segnalazione dell&#39;avanzamento durante la riproduzione.

* **Callback per l&#39;implementazione**`onAdProgress(AdPlaybackEvent event)`

* **Codice** evento `AD_PROGRESS`

`AdResolutionCompleteEventListener`

* **Significato** : risoluzione completa di annunci pubblicitari Primetime. Questo evento è applicabile solo al contenuto VOD.

* **Callback per l&#39;implementazione**`onAdResolutionComplete()`

* **Codice** evento `AD_RESOLUTION_COMPLETE`

`AdStartedEventListener`{#section_A4339C48F82640A8AF4AF09CB3B33188}

* **Significato** La riproduzione dell&#39;annuncio è iniziata.

* **Callback per l&#39;implementazione**`onAdStarted(AdPlaybackEvent event)`

* **Codice** evento `AD_START`

`AudioUpdatedEventListener`

* **Significato** È stata rilevata una nuova traccia audio.

* **Callback per l&#39;implementazione**`onAudioUpdated(MediaPlayerItemEvent event)`

* **Codice** evento `AUDIO_TRACK_UPDATED`

`BufferingBeginEventListener`

* **Significato** Il giocatore ha iniziato a bufferizzare.

* **Callback per l&#39;implementazione**`onBufferingBegin(BufferEvent event)`

* **Codice** evento `BUFFERING_BEGIN`

`BufferingEndEventListener`

* **Significato** Il giocatore ha smesso di bufferizzare.

* **Callback per l&#39;implementazione**`onBufferingEnd(BufferEvent event)`

* **Codice** evento `BUFFERING_END`

&quot;BufferPreparedEventListener&quot;

* **Significato** Il buffer è preparato.

* **Callback per l&#39;implementazione**`onBufferPrepared()`

* **Codice** evento `BUFFER_PREPARED`

`CaptionsUpdatedEventListener`

* **Significato** È stata rilevata una nuova traccia di didascalia.

* **Callback per l&#39;implementazione**`onCaptionsUpdated(MediaPlayerItemEvent event)`

* **Codice** evento `CAPTIONS_UPDATED`

`DRMMetadataInfoEventListener`

* **Significato** Nel flusso multimediale è stato rilevato un nuovo metadati DRM.

* **Callback per l&#39;implementazione**`onDRMMetadataInfo(DRMMetadataInfoEvent event)`

* **Codice** evento `DRM_METADATA`

`ItemCreatedEventListener`

* **Significato** È stato creato un nuovo elemento del lettore multimediale.

* **Callback per l&#39;implementazione**`onItemCreated(MediaPlayerItemEvent event)`

* **Codice** evento `ITEM_CREATED`

`ItemLoadCompleteEventListener`

* **Significato** Nuove informazioni di caricamento create per l&#39;elemento corrente.

* **Callback per l&#39;implementazione**`onLoadComplete(MediaPlayerItemEvent event)`

* **Codice** evento `ITEM_UPDATED`

`LoadInformationEventListener`

* **Significato** È stato caricato un nuovo segmento.

* **Callback per l&#39;implementazione**`onLoadInformation(LoadInformationEvent event)`

* **Codice** evento `LOAD_INFORMATION_AVAILABLE`

`MainManifestUpdatedEventListener`

* **Significato** Il manifesto principale o la playlist è stata aggiornata.

* **Callback per l&#39;implementazione**`onMainManifestUpdated(MediaPlayerItemEvent event)`

* **Codice** evento `MANIFEST_UPDATED`

`NotificationEventListener`

* **Significato** Operazione non riuscita.

* **Callback per l&#39;implementazione**`onNotification(NotificationEvent event)`

* **Codice** evento `OPERATION_FAILED`

`PlaybackRangeUpdatedEventListener`

* **Significato** L&#39;intervallo di riproduzione è stato aggiornato.

* **Callback per l&#39;implementazione**`onPlaybackRangeUpdated(MediaPlayerItemEvent event)`

* **Codice** evento `PLAYBACK_RANGE_UPDATED`

`PlaybackRatePlayingEventListener`

* **Significato** Una nuova frequenza di riproduzione è visibile sullo schermo.

* **Callback per l&#39;implementazione**`onRatePlaying(PlaybackRateEvent event)`

* **Codice** evento `RATE_PLAYING`

`PlaybackRateSelectedEventListener`

* **Significato** L&#39;attributo rate di MediaPlayer è stato impostato.

* **Callback per l&#39;implementazione**`onRateSelected(PlaybackRateEvent event)`

* **Codice** evento `RATE_SELECTED`

`PlayStartEventListener`

* **Significato** La riproduzione è iniziata.

* **Callback per l&#39;implementazione**`onPlayStart()`

* **Codice** evento `PLAY_START`

`ProfileChangeEventListener`

* **Significato** Il profilo corrente di MediaPlayer è cambiato.

* **Callback per l&#39;implementazione**`onProfileChanged(ProfileEvent event)`

* **Codice** evento `PROFILE_CHANGED`

`ReservationReachedEventListener`

* **Significato** : la riproduzione ha raggiunto una prenotazione della timeline.

* **Callback per l&#39;implementazione**`onReservationReached(ReservationEvent event)`

* **Codice** evento `RESERVATION_REACHED`

`SeekBeginEventListener`

* **Significato** Operazione di ricerca avviata.

* **Callback per l&#39;implementazione**`onSeekBegin(SeekEvent event)`

* **Codice** evento `SEEK_BEGIN`

`SeekEndEventListener`

* **Significato** Operazione di ricerca completata.

* **Callback per l&#39;implementazione**`onSeekEnd(SeekEvent event)`

* **Codice** evento `SEEK_END`

`SeekPositionAdjustedEventListener`

* **Significato** La posizione di ricerca è stata modificata a causa delle regole di riproduzione interne o delle regole aziendali esterne.

* **Callback per l&#39;implementazione**`onPositionAdjusted(SeekEvent event)`

* **Codice** evento `SEEK_POSITION_ADJUSTED`

`SizeAvailableEventListener`

* **Significato** Le dimensioni del supporto sono disponibili.

* **Callback per l&#39;implementazione**`onSizeAvailable(SizeAvailableEvent event)`

* **Codice** evento `SIZE_AVAILABLE`

`StatusChangeEventListener`

* **Significato** Lo stato di MediaPlayer è cambiato.

* **Callback per l&#39;implementazione**`onStatusChanged(MediaPlayerStatusChangeEvent event)`

* **Codice** evento `STATUS_CHANGED`

`TimeChangeEventListener`

* **Significato** La testina di riproduzione è cambiata.

* **Callback per l&#39;implementazione**`onTimeChanged(TimeChangeEvent event)`

* **Codice** evento `TIME_CHANGED`

`TimedEventEventListener`

* **Significato** L&#39;operazione è completa con il tempo necessario per l&#39;operazione.

* **Callback per l&#39;implementazione**`onTimedEvent(TimedEventEvent event)`

* **Codice** evento `TIMED_EVENT`

`TimelineMetadataAddedInBackgroundEventListener`

* **Significato** Un nuovo metadati temporizzato è stato aggiunto a un elemento in background.

* **Callback per l&#39;implementazione**`onTimedMetadata(TimedMetadataEvent event)`

* **Codice** evento `TIMED_METADATA_ADDED_IN_BACKGROUND`

`TimedMetadataEventListener`

* **Significato** Nel flusso multimediale è stato rilevato un nuovo metadati temporizzato.

* **Callback per l&#39;implementazione**`onTimedMetadata(TimedMetadataEvent event)`

* **Codice** evento `TIMED_METADATA_AVAILABLE`

`TimelineUpdatedEventListener`

* **Significato** La timeline è stata modificata. Gli annunci potrebbero essere stati aggiunti o rimossi dalla timeline.

* **Callback per l&#39;implementazione**`onTimelineUpdated(TimelineEvent event)`

* **Codice** evento `TIMELINE_UPDATED`