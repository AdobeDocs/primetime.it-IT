---
description: TVSDK invia eventi di riproduzione degli annunci in risposta a operazioni correlate agli annunci, ad esempio all’avvio della riproduzione di un annuncio.
title: Eventi di riproduzione degli annunci
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# Eventi di riproduzione degli annunci{#ad-playback-events}

TVSDK invia eventi di riproduzione degli annunci in risposta a operazioni correlate agli annunci, ad esempio all’avvio della riproduzione di un annuncio.

Per ricevere notifiche su tutti gli eventi relativi alla riproduzione di annunci, registra un’implementazione di `MediaPlayer.AdPlaybackEventListener` inclusi i seguenti callback.

>[!TIP]
>
>Quando gli annunci vengono inseriti o rimossi dal contenuto multimediale, TVSDK invia l’evento di riproduzione [onTimelineUpdated](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onTimelineUpdated()).

| Evento | Significato |
|---|---|
| [onAdBreakComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdBreakComplete(com.adobe.mediacore.timeline.advertising.AdBreak)) (AdBreak adBreak) | Una pausa annuncio è stata riprodotta completamente. |
| onAdBreakSkipped | Un’interruzione pubblicitaria è stata saltata durante la riproduzione. |
| [onAdBreakStart](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdBreakStart(com.adobe.mediacore.timeline.advertising.AdBreak)) (AdBreak adBreak) | È iniziata un’interruzione pubblicitaria. |
| [onAdClick](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdClick(com.adobe.mediacore.timeline.advertising.AdBreak,%20com.adobe.mediacore.timeline.advertising.Ad,%20com.adobe.mediacore.timeline.advertising.AdClick)) (AdBreak, Ad, AdClick, AdClick) | L’utente ha fatto clic sull’annuncio. Fornisce informazioni all’applicazione sull’annuncio su cui l’utente ha fatto clic, in risposta alla chiamata dell’applicazione `notifyClick` il `MediaPlayerView`. |
| [onAdComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdComplete(com.adobe.mediacore.timeline.advertising.AdBreak)) (AdBreak adBreak, Ad ad) | Un annuncio è stato riprodotto completamente. |
| [onAdProgress](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdProgress(com.adobe.mediacore.timeline.advertising.AdBreak,com.adobe.mediacore.timeline.advertising.Ad,%20int)) (AdBreak adBreak, Ad ad, percentuale int) | La riproduzione dell’annuncio è andata avanti. Inviato più volte durante la riproduzione di un annuncio. |
| [onAdStart](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdStart(com.adobe.mediacore.timeline.advertising.AdBreak,%20com.adobe.mediacore.timeline.advertising.Ad)) (AdBreak adBreak, Ad ad) | Un annuncio è stato avviato. |
