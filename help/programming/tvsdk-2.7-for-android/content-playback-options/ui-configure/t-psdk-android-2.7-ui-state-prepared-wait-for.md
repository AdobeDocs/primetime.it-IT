---
description: Prima di poter utilizzare la maggior parte dei metodi del lettore TVSDK, il lettore deve trovarsi in uno stato valido.
title: In attesa di uno stato valido
exl-id: fddb6696-9226-408d-be3c-58d4ce7db55d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# Attesa di uno stato valido {#wait-for-a-valid-state}

Con TVSDK, puoi controllare l’esperienza di riproduzione di base per live e video on-demand (VOD). TVSDK fornisce metodi e proprietà sull’istanza del lettore che è possibile utilizzare per configurare l’interfaccia utente del lettore.

Prima di poter utilizzare la maggior parte dei metodi del lettore TVSDK, il lettore deve trovarsi in uno stato valido.

L’attesa che il lettore sia nello stato corretto assicura che la risorsa multimediale sia stata caricata correttamente. Se il lettore non si trova almeno nello stato richiesto, vengono lanciati molti metodi del lettore `MediaPlayerException`.

Lo stato richiesto è in genere PREPARATO. In questo caso, la routine di callback per `StatusChangeEventListener.onStatusChanged()` viene eseguito.

1. Per confermare che lo stato è `PREPARED`, spunta `MediaPlayer.MediaPlayerStatus`.
