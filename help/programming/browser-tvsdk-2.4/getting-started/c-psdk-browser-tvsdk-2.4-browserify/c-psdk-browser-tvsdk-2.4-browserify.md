---
description: È possibile creare un lettore compatibile con Browserify utilizzando i file JS forniti dal Browser TVSDK.
seo-description: È possibile creare un lettore compatibile con Browserify utilizzando i file JS forniti dal Browser TVSDK.
seo-title: Lettore compatibile con browser
title: Lettore compatibile con browser
uuid: 1832c826-d5d0-41b0-852f-286c8e4fa0f3
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Panoramica {#browserify-compatible-player-overview}

È possibile creare un lettore compatibile con Browserify utilizzando i file JS forniti dal Browser TVSDK.

Browser TVSDK fornisce due file JS compatibili con browser. Uno è utilizzabile con il modulo AdobePSDK; questo è per lo sviluppo di app senza il framework di interfaccia utente. L&#39;altro è destinato all&#39;uso con il modulo UI-Framework; restituisce lo spazio dei nomi PTP utilizzato per la scrittura di app tramite l&#39;interfaccia utente Framework.

Per iniziare a utilizzare Browserify, esegui i seguenti comandi di configurazione per creare [!DNL final.js] i file (il file del bundle Browserify) all&#39;interno delle [!DNL example] directory in [!DNL samples/browerify/reference] e [!DNL samples/browerify/ui-framework]:

1. Passa a [!DNL samples/browserify/reference/build].
1. Eseguite i comandi seguenti:

   1. [!DNL npm install]
   1. [!DNL node_modules/.bin/grunt]

1. Passa a [!DNL samples/browserify/ui-framework/build].
1. Eseguite gli stessi comandi del passaggio 2.

Con questa configurazione, potete procedere alla creazione di app TVSDK compatibili con browser basate sugli esempi forniti con TVSDK.
