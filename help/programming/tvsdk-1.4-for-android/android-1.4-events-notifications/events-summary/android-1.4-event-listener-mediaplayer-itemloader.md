---
description: TVSDK invia gli eventi degli elementi del lettore multimediale in risposta al caricamento di un elemento multimediale.
title: Eventi del caricatore
exl-id: 80a503f2-ad2e-44e5-93dc-2311df77f52e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---

# Eventi del caricatore{#loader-events}

TVSDK invia gli eventi degli elementi del lettore multimediale in risposta al caricamento di un elemento multimediale.

Questi eventi forniscono un flusso di lavoro alternativo. Non è necessario implementare questa interfaccia durante la creazione di un MediaPlayer. Utilizzalo quando vuoi avere un `MediaPlayerItemLoader`.

Per ricevere notifiche su eventi relativi al caricamento di una risorsa del lettore multimediale, registra un’implementazione di `MediaPlayerItemLoader.LoaderListener` inclusi i seguenti eventi.

| Evento | Significato |
|---|---|
| [onLoadComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItemLoader.LoaderListener.html#onLoadComplete(com.adobe.mediacore.MediaPlayerItem))([mediaPlayerItem](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItem.html) playerItem) | Caricamento delle risorse multimediali completato. |
| [onError](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItemLoader.LoaderListener.html#onError(com.adobe.ave.MediaErrorCode,%20java.lang.String)) | Si è verificato un problema con il caricamento delle risorse multimediali. |

>[!NOTE]
>
>Vedi anche `onLoadInfo (loadInfo)` in Eventi QoS.
