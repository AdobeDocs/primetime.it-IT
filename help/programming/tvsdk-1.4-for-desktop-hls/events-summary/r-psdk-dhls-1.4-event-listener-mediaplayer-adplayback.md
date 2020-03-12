---
description: TVSDK invia eventi di riproduzione annunci in risposta a operazioni correlate agli annunci, ad esempio all'avvio della riproduzione di un annuncio.
seo-description: TVSDK invia eventi di riproduzione annunci in risposta a operazioni correlate agli annunci, ad esempio all'avvio della riproduzione di un annuncio.
seo-title: Eventi di riproduzione annunci
title: Eventi di riproduzione annunci
uuid: 63138237-2315-45ff-914d-369da18fdff7
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# Eventi di riproduzione annunci {#ad-playback-events}

TVSDK invia eventi di riproduzione annunci in risposta a operazioni correlate agli annunci, ad esempio all&#39;avvio della riproduzione di un annuncio.

Per ricevere notifiche su tutti gli eventi relativi alla riproduzione di annunci, registrate i listener con l&#39; `MediaPlayer` oggetto per gli eventi seguenti.

>[!TIP]
>
>Quando gli annunci vengono inseriti o rimossi dal supporto, TVSDK invia l’evento di riproduzione TimelineEvent.[TIMELINE_UPDATED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimelineEvent.html#TIMELINE_UPDATED).

| Evento | Significato |
|---|---|
| AdBreakPlaybackEvent.[AD_BREAK_COMPLETED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html#AD_BREAK_COMPLETED) | Una pausa pubblicitaria ha giocato completamente. |
| AdBreakPlaybackEvent.[AD_BREAK_SKIPPED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html#AD_BREAK_SKIPPED) | Durante la riproduzione è stata saltata un&#39;interruzione annuncio. |
| AdBreakPlaybackEvent.[AD_BREAK_STARTED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html#AD_BREAK_STARTED) | È iniziata una pausa pubblicitaria. |
| AdClickEvent.[ANNUNCI _CLICK](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdClickEvent.html#AD_CLICK) | L&#39;utente ha fatto clic sull&#39;annuncio. Fornisce informazioni all&#39;applicazione sull&#39;annuncio che l&#39;utente ha fatto clic, in risposta alla chiamata dell&#39;applicazione `notifyClick` al `MediaPlayerView`. |
| AdPlaybackEvent.[AD_COMPLETO](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_COMPLETED) | Un annuncio ha giocato completamente. |
| AdPlaybackEvent.[AD_PROGRESS](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_PROGRESS) | La riproduzione degli annunci è progredita. Inviato più volte durante la riproduzione di un annuncio. |
| AdPlaybackEvent.[AD_SEEK](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_STARTED) | Una ricerca si è verificata oltre i limiti di un annuncio pubblicitario o all&#39;interno di un annuncio. |
| AdPlaybackEvent.[_AVVIO AD](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_STARTED) | È iniziato un annuncio pubblicitario. |