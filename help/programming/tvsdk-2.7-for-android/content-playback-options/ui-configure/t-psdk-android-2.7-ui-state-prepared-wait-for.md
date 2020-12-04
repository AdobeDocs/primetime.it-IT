---
description: Per poter utilizzare la maggior parte dei metodi del lettore TVSDK, il lettore deve avere uno stato valido.
seo-description: Per poter utilizzare la maggior parte dei metodi del lettore TVSDK, il lettore deve avere uno stato valido.
seo-title: Attendi uno stato valido
title: Attendi uno stato valido
uuid: ffa63ad6-84d3-4eb2-aa99-026418d86528
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 0%

---


# Attendere uno stato valido {#wait-for-a-valid-state}

Con TVSDK, potete controllare l&#39;esperienza di riproduzione di base per video live e video on demand (VOD). TVSDK fornisce metodi e proprietà sull’istanza del lettore che è possibile utilizzare per configurare l’interfaccia utente del lettore.

Per poter utilizzare la maggior parte dei metodi del lettore TVSDK, il lettore deve avere uno stato valido.

In attesa che il lettore sia nello stato corretto, la risorsa multimediale viene caricata correttamente. Se il lettore non ha almeno lo stato richiesto, molti metodi di lettore generano `MediaPlayerException`.

In genere lo stato richiesto è PREPARATO. In questo caso, viene eseguita la routine di callback per `StatusChangeEventListener.onStatusChanged()`.

1. Per confermare che lo stato è `PREPARED`, controllare `MediaPlayer.MediaPlayerStatus`.
