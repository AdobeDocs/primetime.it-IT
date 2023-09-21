---
description: L'oggetto MediaPlayer rappresenta il lettore multimediale. Un elemento MediaPlayerItem rappresenta audio o video sul lettore.
title: Informazioni sulla classe MediaPlayerItem
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---

# Informazioni sulla classe MediaPlayerItem{#about-the-mediaplayeritem-class}

L&#39;oggetto MediaPlayer rappresenta il lettore multimediale. Un elemento MediaPlayerItem rappresenta audio o video sul lettore.

Una volta caricata correttamente una risorsa multimediale, TVSDK crea un’istanza di `MediaPlayerItem` per fornire accesso a tale risorsa.

Il `MediaResource` rappresenta una richiesta inviata dal livello applicazione al `MediaPlayer` per caricare il contenuto.

Il `MediaPlayer` risolve la risorsa multimediale, carica il file manifesto associato e analizza il manifesto. Parte asincrona del processo di caricamento delle risorse. Il `MediaPlayerItem` viene prodotta dopo la risoluzione della risorsa e questa istanza è una versione risolta di una `MediaResource`. TVSDK consente di accedere ai nuovi `MediaPlayerItem` istanza tramite `MediaPlayer.CurrentItem`

>[!TIP]
>
>Prima di accedere all’elemento del lettore multimediale, devi attendere che la risorsa sia stata caricata correttamente.
