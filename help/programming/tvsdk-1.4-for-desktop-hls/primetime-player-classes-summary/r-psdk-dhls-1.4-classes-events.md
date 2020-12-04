---
description: Queste classi descrivono gli eventi che TVSDK invia al lettore multimediale in risposta a varie attività.
seo-description: Queste classi descrivono gli eventi che TVSDK invia al lettore multimediale in risposta a varie attività.
seo-title: Eventi, classi
title: Eventi, classi
uuid: 5e63d43c-6112-4958-b8cd-ccf123affd08
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 0%

---


# Classi Eventi {#events-classes}

Queste classi descrivono gli eventi che TVSDK invia al lettore multimediale in risposta a varie attività.

Pacchetto: [com.adobe.mediacore.events](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/package-detail.html)

| Nome | Significato |
|---|---|
| [AdBreakPlaybackEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html) | Classe. Un&#39;interruzione annuncio è iniziata o completata. |
| [AdClickEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdClickEvent.html) | Classe. L&#39;utente ha fatto clic su un annuncio. |
| [AdPlaybackEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html) | Classe. Il giocatore ha suonato un annuncio. |
| [BufferEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/BufferEvent.html) | Classe. Il lettore ha avviato o interrotto il buffering. |
| [CustomAdEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/CustomAdEvent.html) | Classe. Il lettore visualizza lo stato di caricamento personalizzato degli annunci e può ignorare gli annunci che presentano errori o che richiedono troppo tempo per il caricamento. |
| [DRMMetadataInfoEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/DRMMetadataInfoEvent.html) | Classe. I nuovi metadati DRM sono associati all&#39;elemento corrente. |
| [LoadInformationEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/LoadInformationEvent.html) | Classe. Per il flusso multimediale corrente in fase di riproduzione sono disponibili informazioni sul download. |
| [MediaPlayerItemEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html) | Classe. È stato creato un elemento del lettore multimediale. |
| [MediaPlayerItemLoaderEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemLoaderEvent.html) | Classe. Operazione di caricamento completata. Inviato da `MediaPlayerItemLoader` per inviare una notifica ai client. |
| [MediaPlayerStatusChangeEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerStatusChangeEvent.html) | Classe. Lo stato del lettore multimediale è cambiato. |
| [MediaPlayerViewEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerViewEvent.html) | Classe. È stato fatto clic su `MediaPlayerView`. |
| [PlaybackRateEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/PlaybackRateEvent.html) | Classe. La frequenza di riproduzione del lettore multimediale cambia. |
| [ProfileEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/ProfileEvent.html) | Classe. L&#39;algoritmo di commutazione del bit rate adattivo del lettore multimediale è passato a un altro profilo a causa delle condizioni della rete o della macchina. |
| [SeekEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SeekEvent.html) | Classe. Il lettore ha iniziato la ricerca o l&#39;operazione di ricerca è stata completata. |
| [SizeAvailableEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SizeAvailableEvent.html) | Classe. La dimensione del video è disponibile. |
| [TimeChangeEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimeChangeEvent.html) | Classe. Lo stato del lettore multimediale è cambiato. |
| [TimedMetadataEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimedMetadataEvent.html) | Classe. I metadati temporizzati vengono elaborati dal rilevatore di opportunità. |
| [TimelineEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimelineEvent.html) | Classe. La timeline del lettore multimediale è cambiata. |