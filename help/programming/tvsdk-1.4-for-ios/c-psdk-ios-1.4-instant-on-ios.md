---
description: Il caricamento istantaneo precarica parti del supporto su uno o più canali. Quando un utente seleziona o cambia canale, il contenuto inizia prima perché parte del buffering è già stato completato.
title: Istantanea attiva
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# Istantanea attiva{#instant-on}

Il caricamento istantaneo precarica parti del supporto su uno o più canali. Quando un utente seleziona o cambia canale, il contenuto inizia prima perché parte del buffering è già stato completato.

Quando il lettore si trova nel `PTMediaPlayerStatusReady` stato, chiama `prepareToPlay` per precaricare ed elaborare parte del contenuto per una riproduzione successiva.

>[!TIP]
>
>Se non chiami `prepareToPlay`, chiamata `play` chiamate automatiche `prepareToPlay` prima. Il precaricamento e l’elaborazione vengono completati in questa fase.

TVSDK completa alcune o tutte le seguenti attività per `prepareToPlay`:

* Se la chiave dei metadati `kSyncCookiesWithAVAsset` è impostato, TVSDK effettua una richiesta al file originale M3U8 per sincronizzare i cookie.
* Carica le chiavi di metadati DRM.
* Crea e prepara alcune strutture, elementi o risorse necessarie per la riproduzione del contenuto.

>[!TIP]
>
>Il `PTMediaPlayer` e `PTMediaPlayerItem` `prepareToPlay` i metodi sono uguali. Per evitare la creazione di un `PTMediaPlayer` per ogni risorsa, utilizza `PTMediaPlayerItem` metodo.

Instant-on consente di avviare più istanze del lettore multimediale, o istanze del caricatore di elementi del lettore multimediale, simultaneamente in background e di inserire flussi video in tutte queste istanze. Quando un utente cambia il canale e il flusso viene inserito correttamente nel buffer, chiamando `play` sul nuovo canale avvia prima la riproduzione.
