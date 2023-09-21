---
description: Puoi creare un lettore compatibile con Browserify utilizzando i file JS forniti dal TVSDK del browser.
title: Lettore compatibile con Browserify
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---

# Panoramica {#browserify-compatible-player-overview}

Puoi creare un lettore compatibile con Browserify utilizzando i file JS forniti dal TVSDK del browser.

Browser TVSDK fornisce due file JS compatibili con Browserify. Una è per l’utilizzo con il modulo AdobePSDK; è per lo sviluppo di app senza l’interfaccia utente-Framework. L&#39;altro è da utilizzare con il modulo UI-Framework; restituisce lo spazio dei nomi PTP utilizzato per la scrittura di app tramite UI-Framework.

Per iniziare a usare Browserify, esegui i seguenti comandi di installazione per creare [!DNL final.js] (il file del bundle Browserify) all&#39;interno del [!DNL example] directory in [!DNL samples/browerify/reference] e [!DNL samples/browerify/ui-framework]:

1. Accedi a [!DNL samples/browserify/reference/build].
1. Esegui i seguenti comandi:

   1. [!DNL npm install]
   1. [!DNL node_modules/.bin/grunt]

1. Accedi a [!DNL samples/browserify/ui-framework/build].
1. Eseguire gli stessi comandi del passaggio 2.

Al termine della configurazione, puoi procedere con la creazione di app TVSDK compatibili con Browserify in base agli esempi forniti con TVSDK.
