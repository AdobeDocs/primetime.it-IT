---
description: 'null'
seo-description: 'null'
seo-title: Aggiungi pubblicità
title: Aggiungi pubblicità
uuid: 7762506f-b55e-445d-b8a2-c1208358a370
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Aggiungi pubblicità {#add-advertising}

1. Definite i metadati pubblicitari.

   ```js
   var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
     auditudeSettings.domain = "auditude.com"; 
     auditudeSettings.mediaId = "adbe_tearsofsteel2"; 
     auditudeSettings.zoneId = "123869";
   ```

1. Aggiungete i metadati pubblicitari al `MediaResource`.

   ```js
   var mediaResource =  
     new AdobePSDK.MediaResource(resourceUrl, resourceType, auditudeSettings, false);
   ```

1. Aggiungete le impostazioni alla configurazione e aggiungete un `SpliceOut` parser factory.

   ```js
   var config = new AdobePSDK.MediaPlayerItemConfig(); 
   config.advertisingMetadata = auditudeSettings; 
   config.advertisingFactory = new ExtCueOutContentFactory(auditudeSettings);
   ```

1. Aggiungete la risorsa `ExtCueOutContentFactory` alla sezione libreria.
1. Scaricate il file `ExtCueOutContentFactory.js` dalla sezione libreria e inseritelo nella cartella di lavoro.

   ```js
   <script src= "frameworks/player/dash.min.js"></script> 
   <script src= "frameworks/player/primetimemain.min.js"></script> 
   <script src= "frameworks/player/swfobject.js"></script> 
   <script src= "frameworks/player/primetimeei.min.js"></script> 
   <script src= "ExtCueOutContentFactory.js"></script>
   ```

1. Verificate la configurazione.
