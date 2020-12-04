---
description: L’applicazione può monitorare l’attività nel lettore e lo stato di modifica del lettore ascoltando gli eventi inviati da TVSDK.
seo-description: L’applicazione può monitorare l’attività nel lettore e lo stato di modifica del lettore ascoltando gli eventi inviati da TVSDK.
seo-title: Riepilogo degli eventi del lettore Primetime
title: Riepilogo degli eventi del lettore Primetime
uuid: ed3be4c2-8df3-4d96-a30b-74c196262798
translation-type: tm+mt
source-git-commit: a33e1f290fcf78e6f131910f6037f4803f7be98d
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 0%

---


# Riepilogo eventi del lettore Primetime {#primetime-player-events-summary-overview}

L’applicazione può monitorare l’attività nel lettore e lo stato di modifica del lettore ascoltando gli eventi inviati da TVSDK.

## Eventi {#events}

TVSDK avvisa quando si verificano eventi ai quali l’applicazione deve rispondere. Ogni evento corrisponde a una classe listener, con un metodo di callback che è necessario implementare.

>[!TIP]
>
>I codici evento sono le costanti dell&#39;enum `MediaPlayerEvent`.

## AdBreakCompletedEventListener {#section_D7A74A4EACA44E54806D040491B7D879}

* ** Significato ** La riproduzione dell&#39;interruzione dell&#39;annuncio è completa.

* ** Callback per l&#39;implementazione ** `onAdBreakCompleted(AdBreakPlaybackEvent event)`

* ** Codice evento ** `AD_BREAK_COMPLETE`

## AdBreakSkippedEventListener {#section_7AE5442442484F45B521D3309691C59C}

* ** Significato ** Durante la riproduzione è stata saltata un&#39;interruzione pubblicitaria.

* ** Callback per l&#39;implementazione ** `onAdBreakSkipped(AdBreakPlaybackEvent event)`

* ** Codice evento ** `AD_BREAK_SKIPPED`

## AdBreakStartedEventListener {#section_0D50327621164E3A9C8F3337AA20BDE7}

* ** Significato ** La riproduzione dell&#39;interruzione dell&#39;annuncio è iniziata.

* ** Callback per l&#39;implementazione ** `onAdBreakStarted(AdBreakPlaybackEvent event)`

* ** Codice evento ** `AD_BREAK_START`

## AdClicEventListener {#section_9A6FD39EEDE0460B94FD074B5C2FB9BE}

* ** Significato ** È stato fatto clic su un annuncio durante la riproduzione.

* ** Callback per l&#39;implementazione ** `onAdClicked(AdClickEvent event)`

* ** Codice evento ** `AD_CLICK`

## AdCompletedEventListener {#section_D45EA0B1825145259EAC50A3E6B24BFC}

* ** Significato ** La riproduzione dell&#39;annuncio è completa.

* ** Callback per l&#39;implementazione ** `onAdCompleted(AdPlaybackEvent event)`

* ** Codice evento ** `AD_COMPLETE`

## AdProgressEventListener {#section_C26ACC4B941942B0A24DB06585EF52AB}

* ** Significato ** Segnalazione dell&#39;avanzamento durante la riproduzione.

* ** Callback per l&#39;implementazione ** `onAdProgress(AdPlaybackEvent event)`

* ** Codice evento ** `AD_PROGRESS`

## AdResolutionCompleteEventListener {#section_E9D545408CBA448EA2A8606DA629FB0B}

* ** Significato ** Risoluzione annunci Primetime completi. Questo evento è applicabile solo al contenuto VOD.

* ** Callback per l&#39;implementazione ** `onAdResolutionComplete()`

* ** Codice evento ** `AD_RESOLUTION_COMPLETE`

## AdStartedEventListener {#section_A4339C48F82640A8AF4AF09CB3B33188}

* ** Significato ** La riproduzione dell&#39;annuncio è iniziata.

* ** Callback per l&#39;implementazione ** `onAdStarted(AdPlaybackEvent event)`

* ** Codice evento ** `AD_START`

## AudioUpdatedEventListener {#section_06E1A9F683E1411081CFC6BD30C3B669}

* ** Significato ** È stata rilevata una nuova traccia audio.

* ** Callback per l&#39;implementazione ** `onAudioUpdated(MediaPlayerItemEvent event)`

* ** Codice evento ** `AUDIO_TRACK_UPDATED`

## BufferingBeginEventListener {#section_F8378841149A4801867ADDC7C0A98C57}

* ** Significato ** Il lettore ha iniziato il buffering.

* ** Callback per l&#39;implementazione ** `onBufferingBegin(BufferEvent event)`

* ** Codice evento ** `BUFFERING_BEGIN`

## BufferingEndEventListener {#section_9107E0ED59474F11A04E243C6B117E21}

* ** Significato ** Il lettore ha interrotto il buffering.

* ** Callback per l&#39;implementazione ** `onBufferingEnd(BufferEvent event)`

* ** Codice evento ** `BUFFERING_END`

## BufferPreparedEventListener {#section_F6BFDF525D8B41B7B6E0EFCCE3065811}

* ** Significato ** Il tampone è preparato.

* ** Callback per l&#39;implementazione ** `onBufferPrepared()`

* ** Codice evento ** `BUFFER_PREPARED`

## CaptionsUpdatedEventListener {#section_048BB128ADB747519F02DEDDD1C88B86}

* ** Significato ** È stata rilevata una nuova traccia della didascalia.

* ** Callback per l&#39;implementazione ** `onCaptionsUpdated(MediaPlayerItemEvent event)`

* ** Codice evento ** `CAPTIONS_UPDATED`

## DRMMetadataInfoEventListener {#section_CB55064D305A40D5BBAD09A53D63DB95}

* ** Significato ** È stato rilevato un nuovo metadata DRM nel flusso multimediale.

* ** Callback per l&#39;implementazione ** `onDRMMetadataInfo(DRMMetadataInfoEvent event)`

* ** Codice evento ** `DRM_METADATA`

## ItemCreateEventListener {#section_32A3178664C841008370E8447C978AB2}

* ** Significato ** È stato creato un nuovo elemento del lettore multimediale.

* ** Callback per l&#39;implementazione ** `onItemCreated(MediaPlayerItemEvent event)`

* ** Codice evento ** `ITEM_CREATED`

## ItemLoadCompleteEventListener {#section_E29A3D7D2666461599909BD8E8BA46A7}

* ** Significato ** Sono state create nuove informazioni sul carico per l&#39;elemento corrente.

* ** Callback per l&#39;implementazione ** `onLoadComplete(MediaPlayerItemEvent event)`

* ** Codice evento ** `ITEM_UPDATED`

## LoadInformationEventListener {#section_A986AD83F68446B99EAC888F98B39148}

* ** Significato ** È stato caricato un nuovo segmento.

* ** Callback per l&#39;implementazione ** `onLoadInformation(LoadInformationEvent event)`

* ** Codice evento ** `LOAD_INFORMATION_AVAILABLE`

## MainManifestUpdatedEventListener {#section_73709D121CED48C1B38550135DA55548}

* ** Significato ** Il manifesto principale o la playlist è stata aggiornata.

* ** Callback per l&#39;implementazione ** `onMainManifestUpdated(MediaPlayerItemEvent event)`

* ** Codice evento ** `MANIFEST_UPDATED`

## NotificationEventListener {#section_E8F27B979D374B5D8EA184E23BC17E43}

* ** Significato ** Operazione non riuscita.

* ** Callback per l&#39;implementazione ** `onNotification(NotificationEvent event)`

* ** Codice evento ** `OPERATION_FAILED`

## PlaybackRangeUpdatedEventListener {#section_9072862D7EB842AEA3094DAF911CDF7F}

* ** Significato ** L&#39;intervallo di riproduzione è stato aggiornato.

* ** Callback per l&#39;implementazione ** `onPlaybackRangeUpdated(MediaPlayerItemEvent event)`

* ** Codice evento ** `PLAYBACK_RANGE_UPDATED`

## PlaybackRatePlayingEventListener {#section_548A489ABED44F89BDF29DB9EDD348C5}

* ** Significato ** Una nuova frequenza di riproduzione è visibile sullo schermo.

* ** Callback per l&#39;implementazione ** `onRatePlaying(PlaybackRateEvent event)`

* ** Codice evento ** `RATE_PLAYING`

## PlaybackRateSelectedEventListener {#section_B303BAAFA6D14C1599AD3D7D79D722DD}

* ** Significato ** È stato impostato l&#39;attributo di tasso di MediaPlayer.

* ** Callback per l&#39;implementazione ** `onRateSelected(PlaybackRateEvent event)`

* ** Codice evento ** `RATE_SELECTED`

## PlayStartEventListener {#section_1D54CAE387B243679348A26E65B6A3FD}

* ** Significato ** La riproduzione è iniziata.

* ** Callback per l&#39;implementazione ** `onPlayStart()`

* ** Codice evento ** `PLAY_START`

## ProfileChangeEventListener {#section_EEDF08916D1D40509E64EC180F143C9A}

* ** Significato ** Il profilo corrente di MediaPlayer è cambiato.

* ** Callback per l&#39;implementazione ** `onProfileChanged(ProfileEvent event)`

* ** Codice evento ** `PROFILE_CHANGED`

## ReservationReachedEventListener {#section_31677E931F154E7E86D725B2B046065C}

* ** Significato ** La riproduzione ha raggiunto una prenotazione della timeline.

* ** Callback per l&#39;implementazione ** `onReservationReached(ReservationEvent event)`

* ** Codice evento ** `RESERVATION_REACHED`

## CercaBeginEventListener {#section_749E02ED2B1647438F50224C85260A1D}

* ** Significato ** Operazione di ricerca avviata.

* ** Callback per l&#39;implementazione ** `onSeekBegin(SeekEvent event)`

* ** Codice evento ** `SEEK_BEGIN`

## CercaEndEventListener {#section_4F70BAD695AF4717B2254D9DBA1071E4}

* ** Significato ** L&#39;operazione di ricerca è terminata.

* ** Callback per l&#39;implementazione ** `onSeekEnd(SeekEvent event)`

* ** Codice evento ** `SEEK_END`

## SeekPositionAdjustedEventListener {#section_01F89B73DBB84BEBBA60D820BF5FAC9A}

* ** Significato ** La posizione di ricerca è stata regolata a causa delle regole di riproduzione interne o delle regole aziendali esterne.

* ** Callback per l&#39;implementazione ** `onPositionAdjusted(SeekEvent event)`

* ** Codice evento ** `SEEK_POSITION_ADJUSTED`

## SizeAvailableEventListener {#section_90DF6565E59B44B19338A7B89D53BBBF}

* ** Significato ** La dimensione del supporto è disponibile.

* ** Callback per l&#39;implementazione ** `onSizeAvailable(SizeAvailableEvent event)`

* ** Codice evento ** `SIZE_AVAILABLE`

## StatusChangeEventListener {#section_310D2327089D46358F9CE03EA76F3287}

* ** Significato ** Lo stato di MediaPlayer è cambiato.

* ** Callback per l&#39;implementazione ** `onStatusChanged(MediaPlayerStatusChangeEvent event)`

* ** Codice evento ** `STATUS_CHANGED`

## TimeChangeEventListener {#section_ED3855BD90124D97836B2D0957AD9E0C}

* ** Significato ** La testina di riproduzione è cambiata.

* ** Callback per l&#39;implementazione ** `onTimeChanged(TimeChangeEvent event)`

* ** Codice evento ** `TIME_CHANGED`

## TimedEventEventListener {#section_5E62C2C81C3B4F93B46E7518578456EA}

* ** Significato ** L&#39;operazione è completa con il tempo necessario per l&#39;operazione.

* ** Callback per l&#39;implementazione ** `onTimedEvent(TimedEventEvent event)`

* ** Codice evento ** `TIMED_EVENT`

## TimelineMetadataAddedInBackgroundEventListener {#section_7B923C7116154CCFBAE1FCA92C928EB2}

* ** Significato ** Sono stati aggiunti nuovi metadati temporizzati a un elemento in background.

* ** Callback per l&#39;implementazione ** `onTimedMetadata(TimedMetadataEvent event)`

* ** Codice evento ** `TIMED_METADATA_ADDED_IN_BACKGROUND`

## TimedMetadataEventListener {#section_9741EA321ACF403FB8E9AB311BAACDD7}

* ** Significato ** Nel flusso multimediale è stato rilevato un nuovo metadata temporizzato.

* ** Callback per l&#39;implementazione ** `onTimedMetadata(TimedMetadataEvent event)`

* ** Codice evento ** `TIMED_METADATA_AVAILABLE`

## TimelineUpdatedEventListener {#section_D0755BD2AF3347C7861395706E31B861}

* ** Significato ** La timeline è stata modificata. Gli annunci potrebbero essere stati aggiunti o rimossi dalla timeline.

* ** Callback per l&#39;implementazione ** `onTimelineUpdated(TimelineEvent event)`

* ** Codice evento ** `TIMELINE_UPDATED`