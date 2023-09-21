---
description: Quality of Service (QoS) offre una visualizzazione dettagliata delle prestazioni del motore video. Browser TVSDK fornisce statistiche dettagliate su riproduzione, buffering e dispositivi.
title: Statistiche sulla qualità del servizio
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---

# Statistiche sulla qualità del servizio{#quality-of-service-statistics}

Quality of Service (QoS) offre una visualizzazione dettagliata delle prestazioni del motore video. Browser TVSDK fornisce statistiche dettagliate su riproduzione, buffering e dispositivi.

## Leggi le statistiche su riproduzione, buffering e dispositivo QOS {#read-qos-playback-buffering-and-device-statistics}

È possibile leggere le statistiche di riproduzione, buffering e dispositivo dalla classe QOSProvider.

Il `QOSProvider` class fornisce varie statistiche, tra cui informazioni su buffering, bit rate, frame rate, dati temporali e così via.

1. Crea un&#39;istanza di un lettore multimediale.
1. Creare un `QOSProvider` e collegarlo al lettore multimediale.

   ```js
   // Create Media Player.qosProvider =  
         new AdobePSDK.QOSProvider(); 
   qosProvider.attachMediaPlayer(player);
   ```

1. (Facoltativo) Leggi le statistiche di riproduzione.

   Una soluzione per leggere le statistiche di riproduzione è disporre di un timer, che recupera periodicamente i nuovi valori QoS dalla `QOSProvider`. Ad esempio:

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

1. (Facoltativo) Leggi le informazioni specifiche del dispositivo.

   ```js
   // Show device information 
   DeviceInformation deviceInfo = new QOSProvider().deviceInformation; 
   console.log("OS: "+ deviceInfo.getOS()); 
   console.log("Width: "+ deviceInfo.getWidthPixels() +  
               "Height: "+ deviceInfo.getHeightPixels() );
   ```
