---
description: L'accesso immediato precarica parti del contenuto multimediale su uno o più canali. Dopo che un utente seleziona o commuta i canali, il contenuto viene avviato prima perché alcuni dei buffering sono già stati completati.
title: Immediato
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---


# Instant-on {#instant-on}

L&#39;accesso immediato precarica parti del contenuto multimediale su uno o più canali. Dopo che un utente seleziona o commuta i canali, il contenuto viene avviato prima perché alcuni dei buffering sono già stati completati.

Quando il lettore è nello stato `PTMediaPlayerStatusReady`, chiama `prepareToPlay` per precaricare ed elaborare parte del contenuto per una riproduzione successiva.

>[!TIP]
>
>Se non chiami `prepareToPlay`, la chiamata a `play` chiama automaticamente `prepareToPlay`. Al momento il precaricamento e l’elaborazione vengono completati.

TVSDK completa alcune o tutte le seguenti attività per `prepareToPlay`:

* Se la chiave di metadati `kSyncCookiesWithAVAsset` è impostata, TVSDK invia una richiesta al file M3U8 originale per sincronizzare i cookie.
* Carica le chiavi di metadati DRM.
* Crea e prepara alcune strutture, elementi o risorse necessarie per la riproduzione del contenuto.

>[!TIP]
>
>I metodi `PTMediaPlayer` e `PTMediaPlayerItem` `prepareToPlay` sono uguali. Per evitare di creare un&#39;istanza `PTMediaPlayer` separata per ciascuna risorsa, utilizza il metodo `PTMediaPlayerItem` .

L&#39;accesso istantaneo consente di avviare più istanze del lettore multimediale, o istanze del caricatore di elementi multimediali, simultaneamente in background e in buffer i flussi video in tutte queste istanze. Quando un utente cambia il canale e il flusso è stato bufferizzato correttamente, la chiamata di `play` sul nuovo canale avvia la riproduzione prima.