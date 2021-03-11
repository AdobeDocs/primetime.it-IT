---
description: Utilizza il file della libreria Browserify fornito dal browser TVSDK nella tua app per creare un lettore compatibile con Browserify.
title: Creare un lettore compatibile con browser senza l'interfaccia utente Framework
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---


# Crea un lettore compatibile con browser senza UI-Framework{#create-a-browserify-compatible-player-without-the-ui-framework}

Utilizza il file della libreria Browserify fornito dal browser TVSDK nella tua app per creare un lettore compatibile con Browserify.

L’argomento [](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-tvsdk.md) elenca il set di librerie TVSDK per browser che normalmente vengono incluse quando si crea un lettore video di base. A questo scopo è sufficiente aggiungere tag `script` con attributi `src` che puntano alle librerie.

Il processo è leggermente diverso per la creazione di un lettore compatibile con browserify. A questo scopo, utilizza il comando `require` per includere il file [!DNL AdobePSDK.module.js] (fornito dal TVSDK del browser) nell’app. Questo file raggruppa i file della libreria del lettore di base nell’ordine di dipendenza corretto e restituisce lo spazio dei nomi `AdobePSDK` utilizzato per implementare le funzionalità del lettore.

Il browser TVSDK fornisce il seguente esempio Browserify application and build files in the release package:

* [!DNL [..]/samples/browserify/reference/build/Gruntfile.js]
* [!DNL [..]/samples/browserify/reference/build/package.json]
* [!DNL [..]/samples/browserify/reference/examples/sample.html]
* [!DNL [..]/samples/browserify/reference/examples/sample.js]

Per creare un lettore video compatibile con browser:

1. Richiedi il file di libreria compatibile con Browserify che restituisce lo spazio dei nomi `AdobePSDK`:

   ```
   var AdobePSDK = require('./AdobePSDK.module.js'); 
   var player; 
   function Load () { 
       player = new AdobePSDK.MediaPlayer(); 
   […]
   ```

1. Crea il lettore come descritto in [](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-tvsdk.md).

   Il passaggio 1 in questa attività sostituisce il passaggio nelle istruzioni di base del lettore in cui si sorgente le librerie di base del lettore nel file dell’app.
Ora puoi raggruppare i file dell’app utilizzando la funzione Sfoglia.
