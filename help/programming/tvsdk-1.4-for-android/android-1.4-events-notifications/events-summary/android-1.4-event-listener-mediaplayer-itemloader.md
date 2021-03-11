---
description: TVSDK invia eventi di elementi del lettore multimediale in risposta al caricamento di un elemento multimediale.
title: Eventi di caricamento
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---


# Eventi di caricamento{#loader-events}

TVSDK invia eventi di elementi del lettore multimediale in risposta al caricamento di un elemento multimediale.

Questi eventi forniscono un flusso di lavoro alternativo. Non è necessario implementare questa interfaccia durante la creazione di un MediaPlayer. Utilizzalo quando desideri avere un `MediaPlayerItemLoader`.

Per ricevere notifiche sugli eventi relativi al caricamento di una risorsa del lettore multimediale, registra un’implementazione di `MediaPlayerItemLoader.LoaderListener` inclusi gli eventi seguenti.

| Evento | Significato |
|---|---|
| [onLoadComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItemLoader.LoaderListener.html#onLoadComplete(com.adobe.mediacore.MediaPlayerItem)) ([](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItem.html) mediaPlayerItemPlayerItem) | Caricamento della risorsa multimediale completato. |
| [onError](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItemLoader.LoaderListener.html#onError(com.adobe.ave.MediaErrorCode,%20java.lang.String)) | Si è verificato un problema durante il caricamento della risorsa multimediale. |

>[!NOTE]
>
>Vedi anche `onLoadInfo (loadInfo)` in eventi QoS.

