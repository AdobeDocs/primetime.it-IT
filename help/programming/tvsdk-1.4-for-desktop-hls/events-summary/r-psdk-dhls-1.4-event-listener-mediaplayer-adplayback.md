---
description: TVSDK invia eventi di riproduzione degli annunci in risposta a operazioni correlate agli annunci, ad esempio all’avvio della riproduzione di un annuncio.
title: Eventi di riproduzione degli annunci
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---

# Eventi di riproduzione degli annunci {#ad-playback-events}

TVSDK invia eventi di riproduzione degli annunci in risposta a operazioni correlate agli annunci, ad esempio all’avvio della riproduzione di un annuncio.

Per ricevere notifiche su tutti gli eventi relativi alla riproduzione di annunci, registra i listener con `MediaPlayer` per i seguenti eventi.

>[!TIP]
>
>Quando gli annunci vengono inseriti o rimossi dal contenuto multimediale, TVSDK invia l’evento di riproduzione TimelineEvent.[TIMELINE_UPDATED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimelineEvent.html#TIMELINE_UPDATED).

| Evento | Significato |
|---|---|
| AdBreakPlaybackEvent.[AD_BREAK_COMPLETED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html#AD_BREAK_COMPLETED) | Una pausa annuncio è stata riprodotta completamente. |
| AdBreakPlaybackEvent.[AD_BREAK_SKIPPED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html#AD_BREAK_SKIPPED) | Un’interruzione pubblicitaria è stata saltata durante la riproduzione. |
| AdBreakPlaybackEvent.[AD_BREAK_STARTED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html#AD_BREAK_STARTED) | È iniziata un’interruzione pubblicitaria. |
| AdClickEvent.[AD_CLICK](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdClickEvent.html#AD_CLICK) | L’utente ha fatto clic sull’annuncio. Fornisce informazioni all’applicazione sull’annuncio su cui l’utente ha fatto clic, in risposta alla chiamata dell’applicazione `notifyClick` il `MediaPlayerView`. |
| AdPlaybackEvent.[ANNUNCIO _COMPLETATO](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_COMPLETED) | Un annuncio è stato riprodotto completamente. |
| AdPlaybackEvent.[_AVANZAMENTO ANNUNCIO](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_PROGRESS) | La riproduzione dell’annuncio è andata avanti. Inviato più volte durante la riproduzione di un annuncio. |
| AdPlaybackEvent.[_RICERCA ANNUNCIO](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_STARTED) | Si è verificata una ricerca oltre i limiti dell’annuncio o all’interno di un annuncio. |
| AdPlaybackEvent.[ANNUNCIO _AVVIATO](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_STARTED) | Un annuncio è stato avviato. |
