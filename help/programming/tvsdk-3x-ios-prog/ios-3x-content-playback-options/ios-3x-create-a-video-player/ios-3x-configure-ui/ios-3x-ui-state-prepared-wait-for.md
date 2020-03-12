---
description: Per poter utilizzare la maggior parte dei metodi del lettore TVSDK, il lettore deve avere uno stato valido.
seo-description: Per poter utilizzare la maggior parte dei metodi del lettore TVSDK, il lettore deve avere uno stato valido.
seo-title: Attendere uno stato valido
title: Attendere uno stato valido
uuid: ad9df366-c443-4e6b-a7ab-658d5691eb94
translation-type: tm+mt
source-git-commit: a63768e51c911914a6ba9d884e2587fa34939f9d

---


# Attendere uno stato valido {#wait-for-a-valid-state}

Per poter utilizzare la maggior parte dei metodi del lettore TVSDK, il lettore deve avere uno stato valido.

Il lettore passa attraverso vari stati. In attesa che il lettore sia nello stato corretto, la risorsa multimediale viene caricata correttamente. Se il lettore non ha almeno lo stato richiesto, vengono lanciati molti metodi di lettore `IllegalStateException`.

In genere lo stato richiesto è `PTMediaPlayerStatusReady`.