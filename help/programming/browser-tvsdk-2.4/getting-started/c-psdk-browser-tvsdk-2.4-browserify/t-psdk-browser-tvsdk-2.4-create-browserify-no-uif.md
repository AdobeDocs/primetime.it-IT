---
description: Utilizza il file della libreria Browserify fornito da Browser TVSDK nella tua app, per creare un lettore compatibile con Browserify.
title: Creare un lettore compatibile con Browserify senza UI-Framework
exl-id: 27b5e1c5-49c3-44e4-9e34-0f50a50e36f5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---

# Creare un lettore compatibile con Browserify senza UI-Framework{#create-a-browserify-compatible-player-without-the-ui-framework}

Utilizza il file della libreria Browserify fornito da Browser TVSDK nella tua app, per creare un lettore compatibile con Browserify.

Argomento [](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-tvsdk.md) elenca il set di librerie TVSDK del browser che normalmente includi quando crei un lettore video di base. A questo scopo è sufficiente aggiungere `script` tag con `src` attributi che puntano alle librerie.

Il processo di creazione di un lettore compatibile con Browserify è leggermente diverso. A questo scopo, utilizza `require` comando per includere [!DNL AdobePSDK.module.js] (fornito dal browser TVSDK) nell’app. Questo file raggruppa i file libreria del lettore di base nell’ordine di dipendenza corretto e restituisce `AdobePSDK` namespace utilizzato per implementare le funzioni del lettore.

Browser TVSDK fornisce i seguenti esempi di applicazione Browserify e file di build nel pacchetto di versione:

* [!DNL [...]/samples/browserify/reference/build/Gruntfile.js]
* [!DNL [...]/samples/browserify/reference/build/package.json]
* [!DNL [...]/samples/browserify/reference/examples/sample.html]
* [!DNL [...]/samples/browserify/reference/examples/sample.js]

Per creare un lettore video compatibile con Browserify:

1. Richiedi il file di libreria compatibile con Browserify che restituisce `AdobePSDK` namespace:

   ```
   var AdobePSDK = require('./AdobePSDK.module.js'); 
   var player; 
   function Load () { 
       player = new AdobePSDK.MediaPlayer(); 
   […]
   ```

1. Crea il lettore come descritto in [](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-tvsdk.md).

   Il passaggio 1 di questa attività sostituisce il passaggio nelle istruzioni di base del lettore in cui si originano le singole librerie di base del lettore nel file dell’app.
Ora puoi unire i file dell’app utilizzando Browserify.
