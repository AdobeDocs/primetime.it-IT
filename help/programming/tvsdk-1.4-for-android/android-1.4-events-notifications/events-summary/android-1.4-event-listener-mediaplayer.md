---
description: TVSDK invia eventi di riproduzione di annunci in risposta a operazioni correlate agli annunci, ad esempio quando un annuncio inizia la riproduzione.
title: Eventi di riproduzione di annunci
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---


# Eventi di riproduzione annunci{#ad-playback-events}

TVSDK invia eventi di riproduzione di annunci in risposta a operazioni correlate agli annunci, ad esempio quando un annuncio inizia la riproduzione.

Per ricevere notifiche su tutti gli eventi relativi alla riproduzione di annunci, registra un&#39;implementazione di `MediaPlayer.AdPlaybackEventListener` che include i seguenti callback.

>[!TIP]
>
>Quando gli annunci vengono inseriti o rimossi dal contenuto multimediale, TVSDK invia l&#39;evento di riproduzione [onTimelineUpdated](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onTimelineUpdated()).

| Evento | Significato |
|---|---|
| [onAdBreakComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdBreakComplete(com.adobe.mediacore.timeline.advertising.AdBreak))  (AdBreak adBreak) | Una pausa pubblicitaria ha giocato completamente. |
| onAdBreakSkipped | È stata saltata un&#39;interruzione pubblicitaria durante la riproduzione. |
| [onAdBreakStart](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdBreakStart(com.adobe.mediacore.timeline.advertising.AdBreak))  (AdBreak adBreak) | È iniziata una pausa pubblicitaria. |
| [onAdClick](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdClick(com.adobe.mediacore.timeline.advertising.AdBreak,%20com.adobe.mediacore.timeline.advertising.Ad,%20com.adobe.mediacore.timeline.advertising.AdClick))  (AdBreak adBreak, AdBreak, AdClick, AdClick adClick) | L’utente ha fatto clic sull’annuncio. Fornisce all&#39;applicazione informazioni sull&#39;annuncio che l&#39;utente ha fatto clic, in risposta alla chiamata dell&#39;applicazione `notifyClick` sul `MediaPlayerView`. |
| [onAdComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdComplete(com.adobe.mediacore.timeline.advertising.AdBreak))  (AdBreak adBreak, AdBreak) | Un annuncio ha giocato completamente. |
| [onAdProgress](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdProgress(com.adobe.mediacore.timeline.advertising.AdBreak,com.adobe.mediacore.timeline.advertising.Ad,%20int))  (AdBreak adBreak, AdBreak, AdProgress, int percentuale) | La riproduzione dell&#39;annuncio è progredita. Inviato più volte durante la riproduzione di un annuncio. |
| [onAdStart](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdStart(com.adobe.mediacore.timeline.advertising.AdBreak,%20com.adobe.mediacore.timeline.advertising.Ad))  (AdBreak adBreak, AdBreak) | Un annuncio è iniziato. |