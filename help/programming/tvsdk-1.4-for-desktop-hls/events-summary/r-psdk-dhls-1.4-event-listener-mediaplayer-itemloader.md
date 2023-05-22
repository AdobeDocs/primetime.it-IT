---
description: TVSDK invia gli eventi degli elementi del lettore multimediale in risposta al caricamento di un elemento multimediale.
title: Eventi del caricatore
exl-id: ee5be2d4-5c77-4af4-b8fe-8cef18d7c0d9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---

# Eventi del caricatore{#loader-events}

TVSDK invia gli eventi degli elementi del lettore multimediale in risposta al caricamento di un elemento multimediale.

Questi eventi forniscono un flusso di lavoro alternativo. Non è necessario implementare questa interfaccia durante la creazione di un `MediaPlayer`. Utilizzalo quando vuoi avere un `MediaPlayerItemLoader`.

Per ricevere notifiche sugli eventi correlati al caricamento di una risorsa del lettore multimediale, registra i listener per i seguenti eventi con `MediaPlayerItemLoader` oggetto.

| Evento | Significato |
|---|---|
| MediaPlayerItemLoader.[completato](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerItemLoader.html#event:completed) | Caricamento delle risorse multimediali completato. |
| MediaPlayerItemLoader.[non riuscito](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerItemLoader.html#event:failed) | Si è verificato un problema con il caricamento delle risorse multimediali. |
