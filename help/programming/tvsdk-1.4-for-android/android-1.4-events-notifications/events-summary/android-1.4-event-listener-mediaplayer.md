---
description: TVSDK invia eventi di riproduzione annunci in risposta a operazioni correlate agli annunci, ad esempio all'avvio della riproduzione di un annuncio.
seo-description: TVSDK invia eventi di riproduzione annunci in risposta a operazioni correlate agli annunci, ad esempio all'avvio della riproduzione di un annuncio.
seo-title: Eventi di riproduzione annunci
title: Eventi di riproduzione annunci
uuid: dd6991ae-3e33-4d92-92e9-26b1086a555a
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Eventi di riproduzione annunci{#ad-playback-events}

TVSDK invia eventi di riproduzione annunci in risposta a operazioni correlate agli annunci, ad esempio all&#39;avvio della riproduzione di un annuncio.

Per ricevere notifiche su tutti gli eventi relativi alla riproduzione di annunci, registrate un&#39;implementazione `MediaPlayer.AdPlaybackEventListener` che include le seguenti callback.

>[!TIP]
>
>Quando gli annunci vengono inseriti o rimossi dal supporto, TVSDK invia l’evento di riproduzione [onTimelineUpdated](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onTimelineUpdated()).

| Evento | Significato |
|---|---|
| [onAdBreakComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdBreakComplete(com.adobe.mediacore.timeline.advertising.AdBreak)) (AdBreak adBreak) | Una pausa pubblicitaria ha giocato completamente. |
| onAdBreakSkipped | Durante la riproduzione è stata saltata un&#39;interruzione annuncio. |
| [onAdBreakStart](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdBreakStart(com.adobe.mediacore.timeline.advertising.AdBreak)) (AdBreak adBreak) | È iniziata una pausa pubblicitaria. |
| [onAdClick](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdClick(com.adobe.mediacore.timeline.advertising.AdBreak,%20com.adobe.mediacore.timeline.advertising.Ad,%20com.adobe.mediacore.timeline.advertising.AdClick)) (AdBreak adBreak, AdBreak, AdClick, AdClick adClick) | L&#39;utente ha fatto clic sull&#39;annuncio. Fornisce informazioni all&#39;applicazione sull&#39;annuncio che l&#39;utente ha fatto clic, in risposta alla chiamata dell&#39;applicazione `notifyClick` al `MediaPlayerView`. |
| [onAdComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdComplete(com.adobe.mediacore.timeline.advertising.AdBreak)) (AdBreak adBreak, AdBreak) | Un annuncio ha giocato completamente. |
| [onAdProgress](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdProgress(com.adobe.mediacore.timeline.advertising.AdBreak,com.adobe.mediacore.timeline.advertising.Ad,%20int)) (AdBreak adBreak, AdBreak, AdProgress, percentuale in) | La riproduzione degli annunci è progredita. Inviato più volte durante la riproduzione di un annuncio. |
| [onAdStart](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdStart(com.adobe.mediacore.timeline.advertising.AdBreak,%20com.adobe.mediacore.timeline.advertising.Ad)) (AdBreak adBreak, AdBreak) | È iniziato un annuncio pubblicitario. |