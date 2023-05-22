---
description: Prima di poter utilizzare la maggior parte dei metodi del lettore TVSDK, il lettore deve trovarsi in uno stato valido.
title: Attesa di uno stato valido
exl-id: 2ea7e287-7393-4909-8f55-53cebf4dc289
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---

# Attesa di uno stato valido {#wait-for-a-valid-state}

Prima di poter utilizzare la maggior parte dei metodi del lettore TVSDK, il lettore deve trovarsi in uno stato valido.

Il lettore si sposta attraverso vari stati. L’attesa che il lettore sia nello stato corretto assicura che la risorsa multimediale sia stata caricata correttamente. Se il lettore non si trova almeno nello stato richiesto, vengono lanciati molti metodi del lettore `IllegalStateException`.

Lo stato richiesto è in genere `PTMediaPlayerStatusReady`.
