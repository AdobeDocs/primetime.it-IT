---
description: Utilizzate il file di libreria Browserify fornito da Browser TVSDK nella vostra app per creare un lettore compatibile con Browserify.
seo-description: Utilizzate il file di libreria Browserify fornito da Browser TVSDK nella vostra app per creare un lettore compatibile con Browserify.
seo-title: Creare un lettore compatibile con browserify senza utilizzare l'interfaccia utente Framework
title: Creare un lettore compatibile con browserify senza utilizzare l'interfaccia utente Framework
uuid: c4315bc8-c75d-4dd9-8680-946c1197be1e
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Creare un lettore compatibile con browserify senza utilizzare l&#39;interfaccia utente Framework{#create-a-browserify-compatible-player-without-the-ui-framework}

Utilizzate il file di libreria Browserify fornito da Browser TVSDK nella vostra app per creare un lettore compatibile con Browserify.

L’argomento [](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-tvsdk.md) elenca il set di librerie TVSDK del browser che normalmente includete quando create un lettore video di base. A questo scopo è sufficiente aggiungere `script` tag con `src` attributi che puntano alle librerie.

Il processo è leggermente diverso per la creazione di un lettore compatibile con Browserify. A questo scopo, utilizzate il `require` comando per includere il [!DNL AdobePSDK.module.js] file (fornito dal browser TVSDK) nell&#39;app. Questo file crea il bundle dei file libreria del lettore di base nell&#39;ordine di dipendenza corretto e restituisce lo `AdobePSDK` spazio dei nomi utilizzato per implementare le funzionalità del lettore.

Il browser TVSDK fornisce l&#39;esempio seguente Browserify application and build files in the release package:

* [!DNL [...]/samples/browserify/reference/build/Gruntfile.js]
* [!DNL [...]/samples/browserify/reference/build/package.json]
* [!DNL [...]/samples/browserify/reference/examples/sample.html]
* [!DNL [...]/samples/browserify/reference/examples/sample.js]

Per creare un lettore video compatibile con browser:

1. Richiedi il file di libreria compatibile con Browserify che restituisce lo `AdobePSDK` spazio dei nomi:

   ```
   var AdobePSDK = require('./AdobePSDK.module.js'); 
   var player; 
   function Load () { 
       player = new AdobePSDK.MediaPlayer(); 
   […]
   ```

1. Creare il lettore come descritto in [](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-tvsdk.md).

   Il passaggio 1 di questa attività sostituisce il passaggio delle istruzioni di base del lettore in cui vengono sorgente le singole librerie di base del lettore nel file dell&#39;app.
Ora puoi creare pacchetti di file dell&#39;app utilizzando la funzione di ricerca.
