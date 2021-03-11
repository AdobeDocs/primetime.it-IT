---
description: È possibile creare un lettore compatibile con browser utilizzando i file JS forniti dal TVSDK del browser.
title: Lettore compatibile con browser
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---


# Panoramica {#browserify-compatible-player-overview}

È possibile creare un lettore compatibile con browser utilizzando i file JS forniti dal TVSDK del browser.

Il browser TVSDK fornisce due file JS compatibili con Browserify. Uno è da utilizzare con il modulo AdobePSDK; questo è per lo sviluppo di app senza l&#39;interfaccia utente Framework. L’altro è da utilizzare con il modulo UI-Framework; restituisce lo spazio dei nomi PTP utilizzato per la scrittura di app tramite l’interfaccia utente Framework.

Per iniziare a utilizzare Browserify, esegui i seguenti comandi di configurazione per creare file [!DNL final.js] (il file del bundle Browserify) all&#39;interno delle directory [!DNL example] in [!DNL samples/browerify/reference] e [!DNL samples/browerify/ui-framework]:

1. Passa a [!DNL samples/browserify/reference/build].
1. Esegui i seguenti comandi:

   1. [!DNL npm install]
   1. [!DNL node_modules/.bin/grunt]

1. Passa a [!DNL samples/browserify/ui-framework/build].
1. Esegui gli stessi comandi del passaggio 2.

Al termine della configurazione, puoi procedere alla creazione di app TVSDK compatibili con la ricerca in base agli esempi forniti con TVSDK.
