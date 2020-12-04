---
description: Dopo il corretto caricamento di MediaResource, Browser TVSDK crea un'istanza della classe MediaPlayerItem per fornire l'accesso a tale risorsa.
seo-description: Dopo il corretto caricamento di MediaResource, Browser TVSDK crea un'istanza della classe MediaPlayerItem per fornire l'accesso a tale risorsa.
seo-title: Informazioni sulla classe MediaPlayerItem
title: Informazioni sulla classe MediaPlayerItem
uuid: 5226d3ad-2438-44fe-a8ef-bcc0da8331b8
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---


# Informazioni sulla classe MediaPlayerItem{#about-the-mediaplayeritem-class}

Dopo il corretto caricamento di MediaResource, Browser TVSDK crea un&#39;istanza della classe MediaPlayerItem per fornire l&#39;accesso a tale risorsa.

La `MediaResource` rappresenta una richiesta emessa dal livello applicazione nell&#39;istanza `MediaPlayer` per caricare il contenuto.

La `MediaPlayer` risolve la risorsa multimediale, carica il file manifesto associato e analizza il manifesto. Questa è la parte asincrona del processo di caricamento delle risorse. L&#39;istanza `MediaPlayerItem` viene prodotta dopo che la risorsa è stata risolta e questa è una versione risolta di un `MediaResource`. Browser TVSDK consente di accedere all&#39;istanza appena creata `MediaPlayerItem` tramite `MediaPlayer.CurrentItem`.

>[!TIP]
>
>È necessario attendere che la risorsa venga caricata correttamente prima di accedere all&#39;elemento del lettore multimediale.

