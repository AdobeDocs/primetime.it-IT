---
description: TVSDK invia eventi di riproduzione di annunci in risposta a operazioni correlate agli annunci, ad esempio quando un annuncio inizia la riproduzione.
title: Eventi di riproduzione di annunci
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---


# Eventi di riproduzione annunci {#ad-playback-events}

TVSDK invia eventi di riproduzione di annunci in risposta a operazioni correlate agli annunci, ad esempio quando un annuncio inizia la riproduzione.

Per ricevere notifiche su tutti gli eventi relativi alla riproduzione di annunci, registra i listener con l&#39;oggetto `MediaPlayer` per gli eventi seguenti.

>[!TIP]
>
>Quando gli annunci vengono inseriti o rimossi dal contenuto multimediale, TVSDK invia l’evento di riproduzione TimelineEvent.[TIMELINE_AGGIORNATO](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimelineEvent.html#TIMELINE_UPDATED).

| Evento | Significato |
|---|---|
| AdBreakPlaybackEvent.[AD_BREAK_COMPLETED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html#AD_BREAK_COMPLETED) | Una pausa pubblicitaria ha giocato completamente. |
| AdBreakPlaybackEvent.[AD_BREAK_SKIPPED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html#AD_BREAK_SKIPPED) | È stata saltata un&#39;interruzione pubblicitaria durante la riproduzione. |
| AdBreakPlaybackEvent.[AD_BREAK_STARTED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html#AD_BREAK_STARTED) | È iniziata una pausa pubblicitaria. |
| AdClickEvent.[_FAI CLIC SU ANNUNCI](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdClickEvent.html#AD_CLICK) | L’utente ha fatto clic sull’annuncio. Fornisce all&#39;applicazione informazioni sull&#39;annuncio che l&#39;utente ha fatto clic, in risposta alla chiamata dell&#39;applicazione `notifyClick` sul `MediaPlayerView`. |
| AdPlaybackEvent.[ANNUNCIO _COMPLETATO](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_COMPLETED) | Un annuncio ha giocato completamente. |
| AdPlaybackEvent.[AD_PROGRESS](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_PROGRESS) | La riproduzione dell&#39;annuncio è progredita. Inviato più volte durante la riproduzione di un annuncio. |
| AdPlaybackEvent.[_RICERCA ANNUNCI](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_STARTED) | Una ricerca si è verificata oltre i limiti degli annunci o all&#39;interno di un annuncio. |
| AdPlaybackEvent.[_AVVIO ANNUNCIO](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_STARTED) | Un annuncio è iniziato. |