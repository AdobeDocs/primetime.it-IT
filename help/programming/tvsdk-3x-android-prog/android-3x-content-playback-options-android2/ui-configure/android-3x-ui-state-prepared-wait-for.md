---
description: Prima di poter utilizzare la maggior parte dei metodi del lettore TVSDK, il lettore deve avere uno stato valido.
title: Attendi uno stato valido
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---


# Attendi uno stato valido {#wait-for-a-valid-status}

Con TVSDK, è possibile controllare l&#39;esperienza di riproduzione di base per live e video on demand (VOD). TVSDK fornisce metodi e proprietà sull&#39;istanza del lettore che è possibile utilizzare per configurare l&#39;interfaccia utente del lettore.

Prima di poter utilizzare la maggior parte dei metodi del lettore TVSDK, il lettore deve avere uno stato valido.

In attesa che il lettore sia nello stato corretto, la risorsa multimediale viene caricata correttamente. Se il lettore non ha almeno lo stato richiesto, molti metodi del lettore generano `MediaPlayerException`.

In genere lo stato richiesto è PREPARATO. In questo caso, viene eseguita la routine di callback per `StatusChangeEventListener.onStatusChanged()` .

Per confermare che lo stato è `PREPARED`, controlla `MediaPlayer.MediaPlayerStatus`.