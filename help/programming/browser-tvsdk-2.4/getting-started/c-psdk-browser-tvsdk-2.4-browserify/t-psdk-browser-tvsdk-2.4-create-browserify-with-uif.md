---
description: Utilizzate i file della libreria Browserify forniti da Browser TVSDK nella vostra app per creare un lettore compatibile con Browserify utilizzando il framework dell'interfaccia utente.
seo-description: Utilizzate i file della libreria Browserify forniti da Browser TVSDK nella vostra app per creare un lettore compatibile con Browserify utilizzando il framework dell'interfaccia utente.
seo-title: Creare un lettore compatibile con browserify utilizzando l'interfaccia utente Framework
title: Creare un lettore compatibile con browserify utilizzando l'interfaccia utente Framework
uuid: 544fd872-5ca1-417d-8aab-69613caada0e
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---


# Creare un lettore compatibile con browserify utilizzando l&#39;interfaccia utente Framework {#create-a-browserify-compatible-player-using-the-ui-framework}

Utilizzate i file della libreria Browserify forniti da Browser TVSDK nella vostra app per creare un lettore compatibile con Browserify utilizzando il framework dell&#39;interfaccia utente.

Esempio di file di ricerca inclusi in TVSDK:

* [!DNL [...]/samples/browserify/ui-framework/build/Gruntfile.js]
* [!DNL [...]/samples/browserify/ui-framework/build/package.json]
* [!DNL [...]/samples/browserify/ui-framework/examples/sample.html]
* [!DNL [...]/samples/browserify/ui-framework/examples/sample.js]

Per creare un&#39;app compatibile con Browserify utilizzando l&#39;interfaccia utente Framework, è necessario `require` i due moduli Browserify (forniti da Browser TVSDK) nel codice dell&#39;app:

1. Richiedi moduli di ricerca:

   ```
   var AdobePSDK = require('../../../../frameworks/player/AdobePSDK.module.js');  
   var ptp = require('../../../ui-framework/libs/Primetimevisualapi.module.js);  
   […]
   ```

1. Procedete con lo sviluppo come descritto in [](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-uif.md).
>Ora puoi creare pacchetti di file dell&#39;app utilizzando la funzione di ricerca.
