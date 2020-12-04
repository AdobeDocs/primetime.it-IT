---
description: Consente di precaricare istantaneamente parti del supporto su uno o più canali. Dopo che un utente seleziona o commuta i canali, il contenuto inizia prima perché alcuni dei buffering sono già stati completati.
seo-description: Consente di precaricare istantaneamente parti del supporto su uno o più canali. Dopo che un utente seleziona o commuta i canali, il contenuto inizia prima perché alcuni dei buffering sono già stati completati.
seo-title: Instant-on
title: Instant-on
uuid: 98a5ef79-51e4-474e-a6e8-ca449c430b5e
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---


# Instant-on {#instant-on}

Consente di precaricare istantaneamente parti del supporto su uno o più canali. Dopo che un utente seleziona o commuta i canali, il contenuto inizia prima perché alcuni dei buffering sono già stati completati.

Quando il lettore è nello stato `PTMediaPlayerStatusReady`, chiamare `prepareToPlay` per precaricare ed elaborare parte del contenuto per la riproduzione successiva.

>[!TIP]
>
>Se non si chiama `prepareToPlay`, chiamare `play` automaticamente chiama `prepareToPlay` prima. Al momento il precaricamento e l&#39;elaborazione sono completati.

TVSDK completa alcune o tutte le seguenti attività per `prepareToPlay`:

* Se la chiave di metadati `kSyncCookiesWithAVAsset` è impostata, TVSDK invia una richiesta al file M3U8 originale per sincronizzare i cookie.
* Carica le chiavi di metadati DRM.
* Crea e prepara alcune strutture, elementi o risorse necessarie per la riproduzione del contenuto.

>[!TIP]
>
>I metodi `PTMediaPlayer` e `PTMediaPlayerItem` `prepareToPlay` sono uguali. Per evitare di creare un&#39;istanza `PTMediaPlayer` separata per ciascuna risorsa, utilizzate il metodo `PTMediaPlayerItem`.

L&#39;accesso istantaneo consente di avviare più istanze di lettori multimediali o di caricatori di elementi per lettori multimediali contemporaneamente in background e di creare un buffer dei flussi video in tutte queste istanze. Quando un utente cambia il canale e il flusso si trova correttamente nel buffer, la chiamata di `play` sul nuovo canale avvia la riproduzione prima.