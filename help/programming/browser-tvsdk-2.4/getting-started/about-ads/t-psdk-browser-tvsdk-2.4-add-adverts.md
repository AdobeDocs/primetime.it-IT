---
title: Aggiungi pubblicità
description: Aggiungi pubblicità
copied-description: true
exl-id: 72f875ea-80ae-482b-94be-41116fff3614
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '49'
ht-degree: 0%

---

# Aggiungi pubblicità {#add-advertising}

1. Definisci i metadati pubblicitari.

   ```js
   var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
     auditudeSettings.domain = "auditude.com"; 
     auditudeSettings.mediaId = "adbe_tearsofsteel2"; 
     auditudeSettings.zoneId = "123869";
   ```

1. Aggiungi i metadati pubblicitari al `MediaResource`.

   ```js
   var mediaResource =  
     new AdobePSDK.MediaResource(resourceUrl, resourceType, auditudeSettings, false);
   ```

1. Aggiungi le impostazioni alla configurazione e aggiungi un `SpliceOut` parser factory.

   ```js
   var config = new AdobePSDK.MediaPlayerItemConfig(); 
   config.advertisingMetadata = auditudeSettings; 
   config.advertisingFactory = new ExtCueOutContentFactory(auditudeSettings);
   ```

1. Aggiungi il `ExtCueOutContentFactory` alla sezione libreria.
1. Scarica il file `ExtCueOutContentFactory.js` dalla sezione libreria e inserirla nella cartella di lavoro.

   ```js
   <script src= "frameworks/player/dash.min.js"></script> 
   <script src= "frameworks/player/primetimemain.min.js"></script> 
   <script src= "frameworks/player/swfobject.js"></script> 
   <script src= "frameworks/player/primetimeei.min.js"></script> 
   <script src= "ExtCueOutContentFactory.js"></script>
   ```

1. Verifica la configurazione.
