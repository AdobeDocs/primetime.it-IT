---
description: Per poter utilizzare la maggior parte dei metodi del lettore TVSDK, il lettore deve avere uno stato valido.
seo-description: Per poter utilizzare la maggior parte dei metodi del lettore TVSDK, il lettore deve avere uno stato valido.
seo-title: Attendi uno stato valido
title: Attendi uno stato valido
uuid: 7a86b4cf-f7a0-4d90-9ff2-401640a395c5
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 0%

---


# Attendere uno stato valido {#wait-for-a-valid-status}

Con TVSDK, potete controllare l&#39;esperienza di riproduzione di base per video live e video on demand (VOD). TVSDK fornisce metodi e proprietà sull’istanza del lettore che è possibile utilizzare per configurare l’interfaccia utente del lettore.

Per poter utilizzare la maggior parte dei metodi del lettore TVSDK, il lettore deve avere uno stato valido.

In attesa che il lettore sia nello stato corretto, la risorsa multimediale viene caricata correttamente. Se il lettore non ha almeno lo stato richiesto, molti metodi di lettore generano `MediaPlayerException`.

In genere lo stato richiesto è PREPARATO. In questo caso, viene eseguita la routine di callback per `StatusChangeEventListener.onStatusChanged()`.

Per confermare che lo stato è `PREPARED`, controllare `MediaPlayer.MediaPlayerStatus`.