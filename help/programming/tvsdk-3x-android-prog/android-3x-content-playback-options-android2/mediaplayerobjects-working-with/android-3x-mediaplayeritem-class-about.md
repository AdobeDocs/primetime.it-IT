---
description: Dopo aver caricato correttamente l'oggetto MediaResource, TVSDK crea un'istanza della classe MediaPlayerItem per fornire l'accesso a tale risorsa.
title: Informazioni sulla classe MediaPlayerItem
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 0%

---

# Informazioni sulla classe MediaPlayerItem {#about-the-mediaplayeritem-class}

L&#39;oggetto MediaPlayer rappresenta il lettore multimediale. Un elemento MediaPlayerItem rappresenta audio o video sul lettore.

Dopo aver caricato correttamente l&#39;oggetto MediaResource, TVSDK crea un&#39;istanza della classe MediaPlayerItem per fornire l&#39;accesso a tale risorsa.

Il `MediaResource` rappresenta una richiesta inviata dal livello applicazione al `MediaPlayer` per caricare il contenuto.

Il `MediaPlayer` risolve la risorsa multimediale, carica il file manifesto associato e analizza il manifesto. Parte asincrona del processo di caricamento delle risorse. Il `MediaPlayerItem` viene prodotta dopo la risoluzione della risorsa e questa istanza è una versione risolta di una `MediaResource`. TVSDK consente di accedere ai nuovi `MediaPlayerItem` istanza tramite `MediaPlayer.CurrentItem`.

>[!TIP]
>
>Prima di accedere all’elemento del lettore multimediale, devi attendere che la risorsa sia stata caricata correttamente.
