---
description: Per utilizzare l'Flash Player, accertatevi che l'ambiente soddisfi i requisiti necessari.
seo-description: Per utilizzare l'Flash Player, accertatevi che l'ambiente soddisfi i requisiti necessari.
seo-title: Requisiti di Flash Player
title: Requisiti di Flash Player
uuid: f181457b-2bb4-4baa-b2b7-d787f65fab75
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 1%

---


# Requisiti di Flash Player{#flash-player-requirements}

Per utilizzare l&#39;Flash Player, accertatevi che l&#39;ambiente soddisfi i requisiti necessari.

<!--<a id="section_FEE654D506EC4D85AE77302AD2A27777"></a>-->

I requisiti per il Flash Player sono i seguenti:

* Per riprodurre con `Primetime.js`, installate almeno la versione dell&#39;Flash Player 23.
* Per richiedere gli aggiornamenti alla versione di Flash Player 23 o successiva, installate almeno la versione di Flash Player 11.0.0.

## Requisiti per il pacchetto {#section_F95FC1FEEFEA44D28C9596D2F359AFC7}

La riproduzione con Flash Player richiede i seguenti file SWF:

* Il file SWF principale dell&#39;applicazione che gestisce le API TVSDK del browser.
* Il file SWF `playerProductInstall.swf` che gestisce l&#39;installazione e gli aggiornamenti dei Flash Player.

Inoltre, la riproduzione video nel Flash richiede un file token di autorizzazione che può essere un file SWF o un file `.DAT`. Il percorso dei file SWF, il file del token di autorizzazione, il nome e il tipo del file del token possono essere specificati utilizzando le API AdobePSDK.

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

