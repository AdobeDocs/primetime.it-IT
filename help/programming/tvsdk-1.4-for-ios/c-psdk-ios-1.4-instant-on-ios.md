---
description: Consente di precaricare istantaneamente parti del contenuto multimediale su uno o più canali. Dopo che un utente seleziona o commuta i canali, il contenuto inizia prima perché alcuni dei buffering sono già stati completati.
seo-description: Consente di precaricare istantaneamente parti del contenuto multimediale su uno o più canali. Dopo che un utente seleziona o commuta i canali, il contenuto inizia prima perché alcuni dei buffering sono già stati completati.
seo-title: Instant-on
title: Instant-on
uuid: 23864919-9045-4223-9e47-464e38ebe5ef
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Instant-on{#instant-on}

Consente di precaricare istantaneamente parti del contenuto multimediale su uno o più canali. Dopo che un utente seleziona o commuta i canali, il contenuto inizia prima perché alcuni dei buffering sono già stati completati.

Quando il lettore è nello `PTMediaPlayerStatusReady` stato, chiama `prepareToPlay` per precaricare ed elaborare parte del contenuto per una riproduzione successiva.

>[!TIP]
>
>Se non si chiama `prepareToPlay`, la chiamata `play` automatica chiama `prepareToPlay` per prima. Al momento il precaricamento e l&#39;elaborazione sono completati.

TVSDK completa alcune o tutte le seguenti attività per `prepareToPlay`:

* Se la chiave di metadati `kSyncCookiesWithAVAsset` è impostata, TVSDK invia una richiesta al file M3U8 originale per sincronizzare i cookie.
* Carica le chiavi di metadati DRM.
* Crea e prepara alcune strutture, elementi o risorse necessarie per la riproduzione del contenuto.

>[!TIP]
>
>I `PTMediaPlayer` metodi e `PTMediaPlayerItem``prepareToPlay` sono uguali. Per evitare di creare un’ `PTMediaPlayer` istanza separata per ciascuna risorsa, usate il `PTMediaPlayerItem` metodo .

L&#39;accesso istantaneo consente di avviare più istanze di lettori multimediali o di caricatori di elementi per lettori multimediali contemporaneamente in background e di creare un buffer dei flussi video in tutte queste istanze. Quando un utente cambia il canale e il flusso si trova correttamente nel buffer, richiamando `play` il nuovo canale la riproduzione si avvia prima.
