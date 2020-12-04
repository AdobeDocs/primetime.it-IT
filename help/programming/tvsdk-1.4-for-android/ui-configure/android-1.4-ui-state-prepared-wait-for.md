---
description: Con TVSDK potete controllare l'esperienza di riproduzione di base per video live e video on demand (VOD). TVSDK fornisce metodi e proprietà sull’istanza del lettore che è possibile utilizzare per configurare l’interfaccia utente del lettore.
seo-description: Con TVSDK potete controllare l'esperienza di riproduzione di base per video live e video on demand (VOD). TVSDK fornisce metodi e proprietà sull’istanza del lettore che è possibile utilizzare per configurare l’interfaccia utente del lettore.
seo-title: Attendere uno stato valido
title: Attendere uno stato valido
uuid: 22b68162-1625-4e8a-8566-b0c198155622
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---


# Attendere uno stato valido {#wait-for-a-valid-state}

Con TVSDK potete controllare l&#39;esperienza di riproduzione di base per video live e video on demand (VOD). TVSDK fornisce metodi e proprietà sull’istanza del lettore che è possibile utilizzare per configurare l’interfaccia utente del lettore.

Per poter utilizzare la maggior parte dei metodi del lettore TVSDK, il lettore deve trovarsi in uno stato valido.
Il lettore si sposta attraverso vari stati. In attesa che il lettore sia nello stato corretto, la risorsa multimediale viene caricata correttamente. Se il lettore non è almeno nello stato richiesto, molti metodi di lettore generano `IllegalStateException`.

In genere lo stato richiesto è PREPARATO.
