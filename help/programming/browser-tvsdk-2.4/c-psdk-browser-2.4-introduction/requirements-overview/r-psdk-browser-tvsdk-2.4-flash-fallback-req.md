---
description: Per utilizzare il Flash Player , assicurati che l’ambiente soddisfi i requisiti necessari.
title: Requisiti Flash Player
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 1%

---


# Requisiti di Flash Player{#flash-player-requirements}

Per utilizzare il Flash Player , assicurati che l’ambiente soddisfi i requisiti necessari.

<!--<a id="section_FEE654D506EC4D85AE77302AD2A27777"></a>-->

I requisiti per il Flash Player sono i seguenti:

* Per riprodurre con `Primetime.js`, installa almeno la versione 23 del Flash Player.
* Per ricevere la richiesta di aggiornamenti alla versione 23 o successiva del Flash Player, installa almeno la versione 11.0.0 di Flash Player.

## Requisiti per gli imballaggi {#section_F95FC1FEEFEA44D28C9596D2F359AFC7}

La riproduzione con Flash Player richiede i seguenti file SWF:

* Il file SWF dell&#39;applicazione principale che gestisce le API TVSDK del browser.
* Il file `playerProductInstall.swf` SWF che gestisce l&#39;installazione e gli aggiornamenti del Flash Player.

Inoltre, la riproduzione video nel Flash richiede un file token di autorizzazione che potrebbe essere un file SWF o un file `.DAT`. È possibile specificare il percorso dei file SWF, il file del token di autorizzazione e il nome e il tipo del file del token utilizzando le API AdobePSDK.

Ad esempio:

```js
// Set relative or http path to directory containing SWF.  
// Defaults to current directory for the html page. 
AdobePSDK.setSWFPath(<swfPath>); 
 
// Set the relative or http path to directory containing token file(s). 
// Defaults to SWFPath + "token/". 
AdobePSDK.setAuthorizationTokenPath(<authorizationTokenPath>); 
 
// Set the name of the token file, do not include any path in this string. 
AdobePSDK.setAuthorizationTokenFilename("hlsaf_localhost.swf"); 
 
//Set the token type, "DAT" or "SWF". Defaults to "DAT" 
AdobePSDK.setAuthorizationTokenType("SWF");
```

