---
description: Quality of Service (QoS) offre una visualizzazione dettagliata delle prestazioni del motore video. Browser TVSDK fornisce statistiche dettagliate su riproduzione, buffering e dispositivi.
seo-description: Quality of Service (QoS) offre una visualizzazione dettagliata delle prestazioni del motore video. Browser TVSDK fornisce statistiche dettagliate su riproduzione, buffering e dispositivi.
seo-title: Qualità delle statistiche di servizio
title: Qualità delle statistiche di servizio
uuid: e4bb2617-d8a7-4da7-b669-d6ffab2864bb
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 1%

---


# Statistiche sulla qualità del servizio{#quality-of-service-statistics}

Quality of Service (QoS) offre una visualizzazione dettagliata delle prestazioni del motore video. Browser TVSDK fornisce statistiche dettagliate su riproduzione, buffering e dispositivi.

## Leggi le statistiche relative a riproduzione, buffering e dispositivo QOS {#read-qos-playback-buffering-and-device-statistics}

Dalla classe QOSProvider è possibile leggere le statistiche relative a riproduzione, buffering e dispositivo.

La classe `QOSProvider` fornisce diverse statistiche, tra cui informazioni sul buffering, i bit rate, i frame rate, i dati temporali e così via.

1. Creare un&#39;istanza di un lettore multimediale.
1. Create un oggetto `QOSProvider` e collegatelo al lettore multimediale.

   ```js
   // Create Media Player.qosProvider =  
         new AdobePSDK.QOSProvider(); 
   qosProvider.attachMediaPlayer(player);
   ```

1. (Facoltativo) Leggete le statistiche di riproduzione.

   Una soluzione per leggere le statistiche di riproduzione è avere un timer, che raccoglie periodicamente i nuovi valori QoS dal `QOSProvider`. Ad esempio:

   ```js
   var qosTimer = (function () { 
       var ref = null, 
       qosChangeInterval = 500, // in milliseconds 
   
       startTimer = function () { 
           var playbackInformation = qosProvider.playbackInformation; 
        console.log("Frame rate", playbackInformation.frameRate); 
           console.log ("Dropped frames", playbackInformation.droppedFrameCount); 
           console.log ("Bitrate", playbackInformation.bitrate); 
           console.log ("Buffering time", playbackInformation.bufferingTime); 
           console.log ("Buffer length", playbackInformation.bufferLength); 
           console.log ("Buffer time", playbackInformation.bufferTime); 
           console.log ("Empty buffer count", playbackInformation.emptyBufferCount); 
           console.log ("Time to load", playbackInformation.timeToLoad); 
           console.log ("Time to start", playbackInformation.timeToStart); 
           ref = window.setTimeout(startTimer, qosChangeInterval); 
       }; 
   
       return { 
           start: function () { 
               if (ref !== null) { 
                   // don't start another timeout if one already exists. 
                   return; 
               } 
               startTimer(); 
           }, 
   
           stop: function () { 
               window.clearTimeout(ref); 
               ref = null; 
           } 
       };  
   })() 
   
   qosTimer.start(); 
   ```

1. (Facoltativo) Leggete le informazioni specifiche del dispositivo.

   ```js
   // Show device information 
   DeviceInformation deviceInfo = new QOSProvider().deviceInformation; 
   console.log("OS: "+ deviceInfo.getOS()); 
   console.log("Width: "+ deviceInfo.getWidthPixels() +  
               "Height: "+ deviceInfo.getHeightPixels() );
   ```
