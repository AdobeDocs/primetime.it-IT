---
description: TVSDK invia eventi di elementi del lettore multimediale in risposta al caricamento di un elemento multimediale.
title: Eventi di caricamento
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---


# Eventi di caricamento{#loader-events}

TVSDK invia eventi di elementi del lettore multimediale in risposta al caricamento di un elemento multimediale.

Questi eventi forniscono un flusso di lavoro alternativo. Non è necessario implementare questa interfaccia durante la creazione di un `MediaPlayer`. Utilizzalo quando desideri avere un `MediaPlayerItemLoader`.

Per ricevere notifiche sugli eventi relativi al caricamento di una risorsa del lettore multimediale, registra i listener per i seguenti eventi con l&#39;oggetto `MediaPlayerItemLoader` .

| Evento | Significato |
|---|---|
| MediaPlayerItemLoader.[completato](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerItemLoader.html#event:completed) | Caricamento della risorsa multimediale completato. |
| MediaPlayerItemLoader.[fallito](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerItemLoader.html#event:failed) | Si è verificato un problema durante il caricamento della risorsa multimediale. |