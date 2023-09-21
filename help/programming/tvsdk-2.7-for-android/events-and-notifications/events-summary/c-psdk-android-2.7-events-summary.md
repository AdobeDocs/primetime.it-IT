---
description: L’applicazione può monitorare l’attività nel lettore e il cambiamento dello stato del lettore ascoltando gli eventi inviati da TVSDK.
title: Riepilogo eventi del lettore Primetime
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 0%

---

# Riepilogo eventi del lettore Primetime {#primetime-player-events-summary-overview}

L’applicazione può monitorare l’attività nel lettore e il cambiamento dello stato del lettore ascoltando gli eventi inviati da TVSDK.

## Eventi {#events}

TVSDK notifica quando si verificano eventi ai quali l&#39;applicazione deve rispondere. Ogni evento corrisponde a una classe listener, con un metodo di callback che è necessario implementare.

>[!TIP]
>
>I codici evento sono le costanti del `MediaPlayerEvent` enum.

## AdBreakCompletedEventListener {#section_D7A74A4EACA44E54806D040491B7D879}

* ** Significato ** La riproduzione dell’interruzione pubblicitaria è completa.

* ** callback per implementare ** `onAdBreakCompleted(AdBreakPlaybackEvent event)`

* ** codice evento ** `AD_BREAK_COMPLETE`

## AdBreakSkippedEventListener {#section_7AE5442442484F45B521D3309691C59C}

* ** Significato ** Un’interruzione pubblicitaria è stata saltata durante la riproduzione.

* ** callback per implementare ** `onAdBreakSkipped(AdBreakPlaybackEvent event)`

* ** codice evento ** `AD_BREAK_SKIPPED`

## AdBreakStartedEventListener {#section_0D50327621164E3A9C8F3337AA20BDE7}

* ** Significato ** La riproduzione dell’interruzione pubblicitaria è stata avviata.

* ** callback per implementare ** `onAdBreakStarted(AdBreakPlaybackEvent event)`

* ** codice evento ** `AD_BREAK_START`

## AdClickedEventListener {#section_9A6FD39EEDE0460B94FD074B5C2FB9BE}

* ** Significato ** È stato fatto clic su un annuncio durante la riproduzione.

* ** callback per implementare ** `onAdClicked(AdClickEvent event)`

* ** codice evento ** `AD_CLICK`

## AdCompletedEventListener {#section_D45EA0B1825145259EAC50A3E6B24BFC}

* ** Significato ** La riproduzione dell’annuncio è completa.

* ** callback per implementare ** `onAdCompleted(AdPlaybackEvent event)`

* ** codice evento ** `AD_COMPLETE`

## AdProgressEventListener {#section_C26ACC4B941942B0A24DB06585EF52AB}

* ** Significato ** Avanzamento del reporting durante la riproduzione.

* ** callback per implementare ** `onAdProgress(AdPlaybackEvent event)`

* ** codice evento ** `AD_PROGRESS`

## AdResolutionCompleteEventListener {#section_E9D545408CBA448EA2A8606DA629FB0B}

* ** Significato ** la risoluzione degli annunci Primetime ad decisioningad è completa. Questo evento è applicabile solo al contenuto VOD.

* ** callback per implementare ** `onAdResolutionComplete()`

* ** codice evento ** `AD_RESOLUTION_COMPLETE`

## AdStartedEventListener {#section_A4339C48F82640A8AF4AF09CB3B33188}

* ** Significato ** La riproduzione dell’annuncio è iniziata.

* ** callback per implementare ** `onAdStarted(AdPlaybackEvent event)`

* ** codice evento ** `AD_START`

## AudioUpdatedEventListener {#section_06E1A9F683E1411081CFC6BD30C3B669}

* ** Significato ** È stata rilevata una nuova traccia audio.

* ** callback per implementare ** `onAudioUpdated(MediaPlayerItemEvent event)`

* ** codice evento ** `AUDIO_TRACK_UPDATED`

## BufferingBeginEventListener {#section_F8378841149A4801867ADDC7C0A98C57}

* ** Significato ** Il lettore ha iniziato il buffering.

* ** callback per implementare ** `onBufferingBegin(BufferEvent event)`

* ** codice evento ** `BUFFERING_BEGIN`

## BufferingEndEventListener {#section_9107E0ED59474F11A04E243C6B117E21}

* ** Significato ** Il lettore ha interrotto il buffering.

* ** callback per implementare ** `onBufferingEnd(BufferEvent event)`

* ** codice evento ** `BUFFERING_END`

## BufferPreparedEventListener {#section_F6BFDF525D8B41B7B6E0EFCCE3065811}

* ** Significato ** Preparazione del buffer.

* ** callback per implementare ** `onBufferPrepared()`

* ** codice evento ** `BUFFER_PREPARED`

## SottotitoliAggiornatiEventListener {#section_048BB128ADB747519F02DEDDD1C88B86}

* ** Significato ** È stata rilevata una nuova traccia di didascalia.

* ** callback per implementare ** `onCaptionsUpdated(MediaPlayerItemEvent event)`

* ** codice evento ** `CAPTIONS_UPDATED`

## DRMMetadataInfoEventListener {#section_CB55064D305A40D5BBAD09A53D63DB95}

* ** Significato ** Nel flusso multimediale sono stati rilevati nuovi metadati DRM.

* ** callback per implementare ** `onDRMMetadataInfo(DRMMetadataInfoEvent event)`

* ** codice evento ** `DRM_METADATA`

## ItemCreatedEventListener {#section_32A3178664C841008370E8447C978AB2}

* ** Significato ** È stato creato un nuovo elemento del lettore multimediale.

* ** callback per implementare ** `onItemCreated(MediaPlayerItemEvent event)`

* ** codice evento ** `ITEM_CREATED`

## ItemLoadCompleteEventListener {#section_E29A3D7D2666461599909BD8E8BA46A7}

* ** Significato ** sono state create nuove informazioni di caricamento per l&#39;elemento corrente.

* ** callback per implementare ** `onLoadComplete(MediaPlayerItemEvent event)`

* ** codice evento ** `ITEM_UPDATED`

## LoadInformationEventListener {#section_A986AD83F68446B99EAC888F98B39148}

* ** Significato ** È stato caricato un nuovo segmento.

* ** callback per implementare ** `onLoadInformation(LoadInformationEvent event)`

* ** codice evento ** `LOAD_INFORMATION_AVAILABLE`

## MainManifestUpdatedEventListener {#section_73709D121CED48C1B38550135DA55548}

* ** Significato ** Il manifesto principale o la playlist è stata aggiornata.

* ** callback per implementare ** `onMainManifestUpdated(MediaPlayerItemEvent event)`

* ** codice evento ** `MANIFEST_UPDATED`

## NotificationEventListener {#section_E8F27B979D374B5D8EA184E23BC17E43}

* ** Significato ** Operazione non riuscita.

* ** callback per implementare ** `onNotification(NotificationEvent event)`

* ** codice evento ** `OPERATION_FAILED`

## PlaybackRangeUpdatedEventListener {#section_9072862D7EB842AEA3094DAF911CDF7F}

* ** Significato ** L’intervallo di riproduzione è stato aggiornato.

* ** callback per implementare ** `onPlaybackRangeUpdated(MediaPlayerItemEvent event)`

* ** codice evento ** `PLAYBACK_RANGE_UPDATED`

## PlaybackRatePlayingEventListener {#section_548A489ABED44F89BDF29DB9EDD348C5}

* ** Significato ** Sullo schermo è visibile una nuova velocità di riproduzione.

* ** callback per implementare ** `onRatePlaying(PlaybackRateEvent event)`

* ** codice evento ** `RATE_PLAYING`

## PlaybackRateSelectedEventListener {#section_B303BAAFA6D14C1599AD3D7D79D722DD}

* ** Significato ** È stato impostato l&#39;attributo della tariffa di MediaPlayer.

* ** callback per implementare ** `onRateSelected(PlaybackRateEvent event)`

* ** codice evento ** `RATE_SELECTED`

## PlayStartEventListener {#section_1D54CAE387B243679348A26E65B6A3FD}

* ** Significato ** La riproduzione è iniziata.

* ** callback per implementare ** `onPlayStart()`

* ** codice evento ** `PLAY_START`

## ProfileChangeEventListener {#section_EEDF08916D1D40509E64EC180F143C9A}

* ** Significato ** Il profilo corrente di MediaPlayer è stato modificato.

* ** callback per implementare ** `onProfileChanged(ProfileEvent event)`

* ** codice evento ** `PROFILE_CHANGED`

## ReservationReachedEventListener {#section_31677E931F154E7E86D725B2B046065C}

* ** Significato ** la riproduzione ha raggiunto una prenotazione della timeline.

* ** callback per implementare ** `onReservationReached(ReservationEvent event)`

* ** codice evento ** `RESERVATION_REACHED`

## SeekBeginEventListener {#section_749E02ED2B1647438F50224C85260A1D}

* ** Significato ** operazione di ricerca avviata.

* ** callback per implementare ** `onSeekBegin(SeekEvent event)`

* ** codice evento ** `SEEK_BEGIN`

## SeekEndEventListener {#section_4F70BAD695AF4717B2254D9DBA1071E4}

* ** Significato ** Operazione di ricerca completata.

* ** callback per implementare ** `onSeekEnd(SeekEvent event)`

* ** codice evento ** `SEEK_END`

## SeekPositionAdjustedEventListener {#section_01F89B73DBB84BEBBA60D820BF5FAC9A}

* ** Significato ** La posizione di ricerca è stata regolata a causa di regole di riproduzione interne o regole aziendali esterne.

* ** callback per implementare ** `onPositionAdjusted(SeekEvent event)`

* ** codice evento ** `SEEK_POSITION_ADJUSTED`

## SizeAvailableEventListener {#section_90DF6565E59B44B19338A7B89D53BBBF}

* ** Significato ** È disponibile la dimensione del supporto.

* ** callback per implementare ** `onSizeAvailable(SizeAvailableEvent event)`

* ** codice evento ** `SIZE_AVAILABLE`

## StatusChangeEventListener {#section_310D2327089D46358F9CE03EA76F3287}

* ** Significato ** lo stato di MediaPlayer è cambiato.

* ** callback per implementare ** `onStatusChanged(MediaPlayerStatusChangeEvent event)`

* ** codice evento ** `STATUS_CHANGED`

## TimeChangeEventListener {#section_ED3855BD90124D97836B2D0957AD9E0C}

* ** Significato ** La testina di riproduzione è cambiata.

* ** callback per implementare ** `onTimeChanged(TimeChangeEvent event)`

* ** codice evento ** `TIME_CHANGED`

## TimedEventEventListener {#section_5E62C2C81C3B4F93B46E7518578456EA}

* ** Significato ** L&#39;operazione è completata con il tempo necessario per l&#39;operazione.

* ** callback per implementare ** `onTimedEvent(TimedEventEvent event)`

* ** codice evento ** `TIMED_EVENT`

## TimelineMetadataAddedInBackgroundEventListener {#section_7B923C7116154CCFBAE1FCA92C928EB2}

* ** Significato ** Sono stati aggiunti nuovi metadati temporizzati a un elemento in background.

* ** callback per implementare ** `onTimedMetadata(TimedMetadataEvent event)`

* ** codice evento ** `TIMED_METADATA_ADDED_IN_BACKGROUND`

## TimedMetadataEventListener {#section_9741EA321ACF403FB8E9AB311BAACDD7}

* ** Significato ** Nel flusso multimediale sono stati rilevati nuovi metadati temporizzati.

* ** callback per implementare ** `onTimedMetadata(TimedMetadataEvent event)`

* ** codice evento ** `TIMED_METADATA_AVAILABLE`

## TimelineUpdatedEventListener {#section_D0755BD2AF3347C7861395706E31B861}

* ** Significato ** La timeline è stata modificata. Gli annunci potrebbero essere stati aggiunti o rimossi dalla timeline.

* ** callback per implementare ** `onTimelineUpdated(TimelineEvent event)`

* ** codice evento ** `TIMELINE_UPDATED`
