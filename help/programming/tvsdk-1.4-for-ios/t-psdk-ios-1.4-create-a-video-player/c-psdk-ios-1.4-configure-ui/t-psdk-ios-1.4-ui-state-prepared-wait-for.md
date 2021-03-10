---
description: Prima di poter utilizzare la maggior parte dei metodi del lettore TVSDK, il lettore deve avere uno stato valido.
title: Attendi uno stato valido
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---


# Attendi uno stato valido{#wait-for-a-valid-state}

Prima di poter utilizzare la maggior parte dei metodi del lettore TVSDK, il lettore deve avere uno stato valido.

Il lettore passa attraverso vari stati. In attesa che il lettore sia nello stato corretto, la risorsa multimediale viene caricata correttamente. Se il lettore non ha almeno lo stato richiesto, molti metodi del lettore generano `IllegalStateException`.

In genere lo stato richiesto è `PTMediaPlayerStatusReady`.
