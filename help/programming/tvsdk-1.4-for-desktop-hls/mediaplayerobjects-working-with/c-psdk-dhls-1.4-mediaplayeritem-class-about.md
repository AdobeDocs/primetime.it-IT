---
description: L'oggetto MediaPlayer rappresenta il lettore multimediale. Un elemento MediaPlayerItem rappresenta l’audio o il video sul lettore.
seo-description: L'oggetto MediaPlayer rappresenta il lettore multimediale. Un elemento MediaPlayerItem rappresenta l’audio o il video sul lettore.
seo-title: Informazioni sulla classe MediaPlayerItem
title: Informazioni sulla classe MediaPlayerItem
uuid: 531dd1a6-d72c-4ae3-9c3f-2f1d854245c5
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Informazioni sulla classe MediaPlayerItem{#about-the-mediaplayeritem-class}

L&#39;oggetto MediaPlayer rappresenta il lettore multimediale. Un elemento MediaPlayerItem rappresenta l’audio o il video sul lettore.

<!--<a id="section_01BC89E5C5A94D0A95EF9D29FBCE758A"></a>-->

Dopo che una risorsa multimediale è stata caricata correttamente, TVSDK crea un&#39;istanza della `MediaPlayerItem` classe per fornire l&#39;accesso a tale risorsa.

Rappresenta `MediaResource` una richiesta emessa dal livello applicazione nell’ `MediaPlayer` istanza per caricare il contenuto.

Consente di `MediaPlayer` risolvere la risorsa multimediale, caricare il file manifesto associato e analizzare il manifesto. Questa è la parte asincrona del processo di caricamento delle risorse. L’ `MediaPlayerItem` istanza viene prodotta dopo che la risorsa è stata risolta e questa è una versione risolta di un `MediaResource`. TVSDK consente di accedere all’ `MediaPlayerItem` istanza appena creata tramite `MediaPlayer.currentItem`.

>[!TIP]
>
>È necessario attendere che la risorsa venga caricata correttamente prima di accedere all&#39;elemento del lettore multimediale.

