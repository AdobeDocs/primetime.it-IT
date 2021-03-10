---
description: Utilizza i file della libreria Browserify forniti dal TVSDK del browser nella tua app per creare un lettore compatibile con Browserify utilizzando il framework dell'interfaccia utente.
title: Creare un lettore compatibile con browser utilizzando l'interfaccia utente Framework
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 0%

---


# Crea un lettore compatibile con browser utilizzando l&#39;interfaccia utente Framework {#create-a-browserify-compatible-player-using-the-ui-framework}

Utilizza i file della libreria Browserify forniti dal TVSDK del browser nella tua app per creare un lettore compatibile con Browserify utilizzando il framework dell&#39;interfaccia utente.

File di ricerca di esempio inclusi nel TVSDK:

* [!DNL [..]/samples/browserify/ui-framework/build/Gruntfile.js]
* [!DNL [..]/samples/browserify/ui-framework/build/package.json]
* [!DNL [..]/samples/browserify/ui-framework/examples/sample.html]
* [!DNL [..]/samples/browserify/ui-framework/examples/sample.js]

Per creare un’app compatibile con browser utilizzando l’interfaccia utente Framework, devi `require` inserire i due moduli di ricerca (forniti dal browser TVSDK) nel codice dell’app:

1. Richiedi moduli di ricerca:

   ```
   var AdobePSDK = require('../../../../frameworks/player/AdobePSDK.module.js');  
   var ptp = require('../../../ui-framework/libs/Primetimevisualapi.module.js);  
   […]
   ```

1. Procedi con lo sviluppo come descritto in [](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-uif.md).
>Ora puoi raggruppare i file dell’app utilizzando la funzione Sfoglia.
