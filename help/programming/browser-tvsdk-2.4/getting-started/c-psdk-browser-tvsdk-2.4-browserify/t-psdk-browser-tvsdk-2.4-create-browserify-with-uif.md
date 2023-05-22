---
description: Utilizza i file della libreria Browserify forniti dal Browser TVSDK nella tua app per creare un lettore compatibile con Browserify utilizzando l’interfaccia utente-Framework.
title: Creare un lettore compatibile con Browserify utilizzando UI-Framework
exl-id: cd72cae1-f67e-4192-9a7e-1c1492d88922
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 0%

---

# Creare un lettore compatibile con Browserify utilizzando UI-Framework {#create-a-browserify-compatible-player-using-the-ui-framework}

Utilizza i file della libreria Browserify forniti dal Browser TVSDK nella tua app per creare un lettore compatibile con Browserify utilizzando l’interfaccia utente-Framework.

Esempio di file Browserify inclusi in TVSDK:

* [!DNL [...]/samples/browserify/ui-framework/build/Gruntfile.js]
* [!DNL [...]/samples/browserify/ui-framework/build/package.json]
* [!DNL [...]/samples/browserify/ui-framework/examples/sample.html]
* [!DNL [...]/samples/browserify/ui-framework/examples/sample.js]

Per creare un’app compatibile con Browserify tramite UI-Framework, è necessario `require` i due moduli Browserify (forniti da Browser TVSDK) nel codice dell’app:

1. Richiedi moduli Browserify:

   ```
   var AdobePSDK = require('../../../../frameworks/player/AdobePSDK.module.js');  
   var ptp = require('../../../ui-framework/libs/Primetimevisualapi.module.js);  
   […]
   ```

1. Procedi con lo sviluppo come descritto in [](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-uif.md).
>Ora puoi unire i file dell’app utilizzando Browserify.
