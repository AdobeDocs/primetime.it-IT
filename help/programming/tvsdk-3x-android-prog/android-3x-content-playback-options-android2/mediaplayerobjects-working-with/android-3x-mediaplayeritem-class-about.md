---
description: Dopo aver caricato correttamente l'oggetto MediaResource, TVSDK crea un'istanza della classe MediaPlayerItem per fornire l'accesso a tale risorsa.
seo-description: Dopo aver caricato correttamente l'oggetto MediaResource, TVSDK crea un'istanza della classe MediaPlayerItem per fornire l'accesso a tale risorsa.
seo-title: Informazioni sulla classe MediaPlayerItem
title: Informazioni sulla classe MediaPlayerItem
uuid: fc79c442-2e38-48c4-8ef9-6dce9ad6790a
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Informazioni sulla classe MediaPlayerItem {#about-the-mediaplayeritem-class}

L&#39;oggetto MediaPlayer rappresenta il lettore multimediale. Un elemento MediaPlayerItem rappresenta l’audio o il video sul lettore.

Dopo aver caricato correttamente l&#39;oggetto MediaResource, TVSDK crea un&#39;istanza della classe MediaPlayerItem per fornire l&#39;accesso a tale risorsa.

Rappresenta `MediaResource` una richiesta emessa dal livello applicazione nell’ `MediaPlayer` istanza per caricare il contenuto.

Consente di `MediaPlayer` risolvere la risorsa multimediale, caricare il file manifesto associato e analizzare il manifesto. Questa è la parte asincrona del processo di caricamento delle risorse. L’ `MediaPlayerItem` istanza viene prodotta dopo che la risorsa è stata risolta e questa è una versione risolta di un `MediaResource`. TVSDK consente di accedere all’ `MediaPlayerItem` istanza appena creata tramite `MediaPlayer.CurrentItem`.

>[!TIP]
>
>È necessario attendere che la risorsa venga caricata correttamente prima di accedere all&#39;elemento del lettore multimediale.