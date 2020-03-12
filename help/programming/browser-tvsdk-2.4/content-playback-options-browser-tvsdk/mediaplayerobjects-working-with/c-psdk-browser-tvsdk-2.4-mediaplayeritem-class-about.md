---
description: Dopo il corretto caricamento di MediaResource, Browser TVSDK crea un'istanza della classe MediaPlayerItem per fornire l'accesso a tale risorsa.
seo-description: Dopo il corretto caricamento di MediaResource, Browser TVSDK crea un'istanza della classe MediaPlayerItem per fornire l'accesso a tale risorsa.
seo-title: Informazioni sulla classe MediaPlayerItem
title: Informazioni sulla classe MediaPlayerItem
uuid: 5226d3ad-2438-44fe-a8ef-bcc0da8331b8
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Informazioni sulla classe MediaPlayerItem{#about-the-mediaplayeritem-class}

Dopo il corretto caricamento di MediaResource, Browser TVSDK crea un&#39;istanza della classe MediaPlayerItem per fornire l&#39;accesso a tale risorsa.

Rappresenta `MediaResource` una richiesta emessa dal livello applicazione nell’ `MediaPlayer` istanza per caricare il contenuto.

Consente di `MediaPlayer` risolvere la risorsa multimediale, caricare il file manifesto associato e analizzare il manifesto. Questa è la parte asincrona del processo di caricamento delle risorse. L’ `MediaPlayerItem` istanza viene prodotta dopo che la risorsa è stata risolta e questa è una versione risolta di un `MediaResource`. Browser TVSDK fornisce l&#39;accesso all&#39; `MediaPlayerItem` istanza appena creata attraverso `MediaPlayer.CurrentItem`.

>[!TIP]
>
>È necessario attendere che la risorsa venga caricata correttamente prima di accedere all&#39;elemento del lettore multimediale.

