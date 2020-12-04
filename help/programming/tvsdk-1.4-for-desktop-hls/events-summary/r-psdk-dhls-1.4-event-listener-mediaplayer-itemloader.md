---
description: TVSDK invia eventi di elementi del lettore multimediale in risposta al caricamento di un elemento multimediale.
seo-description: TVSDK invia eventi di elementi del lettore multimediale in risposta al caricamento di un elemento multimediale.
seo-title: Eventi di caricamento
title: Eventi di caricamento
uuid: 0ad37715-14b1-457c-892f-0db0d6220f0c
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---


# Eventi di caricamento{#loader-events}

TVSDK invia eventi di elementi del lettore multimediale in risposta al caricamento di un elemento multimediale.

Questi eventi forniscono un flusso di lavoro alternativo. Non è necessario implementare questa interfaccia durante la creazione di un `MediaPlayer`. Utilizzate questo parametro per ottenere un `MediaPlayerItemLoader`.

Per ricevere notifiche sugli eventi relativi al caricamento di una risorsa del lettore multimediale, registrare i listener per i seguenti eventi con l&#39;oggetto `MediaPlayerItemLoader`.

| Evento | Significato |
|---|---|
| MediaPlayerItemLoader.[completato](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerItemLoader.html#event:completed) | Caricamento della risorsa multimediale completato. |
| MediaPlayerItemLoader.[not](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerItemLoader.html#event:failed) | Si è verificato un problema con il caricamento delle risorse multimediali. |