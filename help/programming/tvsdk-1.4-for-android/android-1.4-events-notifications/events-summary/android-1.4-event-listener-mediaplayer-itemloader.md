---
description: TVSDK invia eventi di elementi del lettore multimediale in risposta al caricamento di un elemento multimediale.
seo-description: TVSDK invia eventi di elementi del lettore multimediale in risposta al caricamento di un elemento multimediale.
seo-title: Eventi di caricamento
title: Eventi di caricamento
uuid: 1b401ff5-4313-4c64-8be9-99bdeb58ba2a
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---


# Eventi di caricamento{#loader-events}

TVSDK invia eventi di elementi del lettore multimediale in risposta al caricamento di un elemento multimediale.

Questi eventi forniscono un flusso di lavoro alternativo. Non è necessario implementare questa interfaccia durante la creazione di un MediaPlayer. Utilizzate questo parametro per ottenere un `MediaPlayerItemLoader`.

Per ricevere notifiche sugli eventi relativi al caricamento di una risorsa Media Player, registrare un&#39;implementazione di `MediaPlayerItemLoader.LoaderListener`, compresi gli eventi seguenti.

| Evento | Significato |
|---|---|
| [onLoadComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItemLoader.LoaderListener.html#onLoadComplete(com.adobe.mediacore.MediaPlayerItem))([](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItem.html) mediaPlayerItemItem) | Caricamento della risorsa multimediale completato. |
| [onError](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItemLoader.LoaderListener.html#onError(com.adobe.ave.MediaErrorCode,%20java.lang.String)) | Si è verificato un problema con il caricamento delle risorse multimediali. |

>[!NOTE]
>
>Vedere anche `onLoadInfo (loadInfo)` in Eventi QoS.

