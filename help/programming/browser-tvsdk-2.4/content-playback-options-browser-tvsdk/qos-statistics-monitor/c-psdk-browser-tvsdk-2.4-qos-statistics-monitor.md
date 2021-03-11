---
description: Quality of Service (QoS) offre una visualizzazione dettagliata delle prestazioni del motore video. Il browser TVSDK fornisce statistiche dettagliate sulla riproduzione, il buffering e i dispositivi.
title: Qualità delle statistiche del servizio
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 1%

---


# Statistiche sulla qualità del servizio{#quality-of-service-statistics}

Quality of Service (QoS) offre una visualizzazione dettagliata delle prestazioni del motore video. Il browser TVSDK fornisce statistiche dettagliate sulla riproduzione, il buffering e i dispositivi.

## Leggi le statistiche relative a riproduzione, buffering e dispositivo QOS {#read-qos-playback-buffering-and-device-statistics}

È possibile leggere le statistiche di riproduzione, buffering e dispositivo dalla classe QOSProvider.

La classe `QOSProvider` fornisce diverse statistiche, tra cui buffering, bit rate, frame rate, dati temporali e così via.

1. Creare un&#39;istanza di un lettore multimediale.
1. Crea un oggetto `QOSProvider` e allegalo al lettore multimediale.

   ```js
   // Create Media Player.qosProvider =  
         new AdobePSDK.QOSProvider(); 
   qosProvider.attachMediaPlayer(player);
   ```

1. (Facoltativo) Leggere le statistiche di riproduzione.

   Una soluzione per leggere le statistiche di riproduzione è avere un timer, che recupera periodicamente i nuovi valori QoS dal `QOSProvider`. Ad esempio:

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
