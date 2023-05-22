---
description: Per utilizzare il Flash Player, assicurati che l’ambiente soddisfi i requisiti necessari.
title: Requisiti Flash Player
exl-id: 26531d0d-d34c-4134-8a05-0604f00a3107
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---

# Requisiti Flash Player{#flash-player-requirements}

Per utilizzare il Flash Player, assicurati che l’ambiente soddisfi i requisiti necessari.

<!--<a id="section_FEE654D506EC4D85AE77302AD2A27777"></a>-->

Di seguito sono riportati i requisiti del Flash Player:

* Per riprodurre con `Primetime.js`, installare almeno la versione di Flash Player 23.
* Per richiedere aggiornamenti al Flash Player versione 23 o successiva, installare almeno Flash Player versione 11.0.0.

## Requisiti di imballaggio {#section_F95FC1FEEFEA44D28C9596D2F359AFC7}

La riproduzione con il Flash Player richiede i seguenti file SWF:

* Il file SWF dell’applicazione principale che gestisce le API TVSDK del browser.
* Il `playerProductInstall.swf` File SWF che gestisce l&#39;installazione e gli aggiornamenti del Flash Player.

Inoltre, la riproduzione video nel Flash richiede un file token di autorizzazione che potrebbe essere un SWF o un `.DAT` file. È possibile specificare il percorso dei file SWF, il file del token di autorizzazione, il nome e il tipo del file token utilizzando le API AdobePSDK.

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
