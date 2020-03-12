---
description: Dalla classe QOSProvider è possibile leggere le statistiche relative a riproduzione, buffering e dispositivo.
seo-description: Dalla classe QOSProvider è possibile leggere le statistiche relative a riproduzione, buffering e dispositivo.
seo-title: Lettura delle statistiche relative a riproduzione, buffering e dispositivo QOS
title: Lettura delle statistiche relative a riproduzione, buffering e dispositivo QOS
uuid: 5ee631fc-cd6f-4f35-8621-2ffdc51a57c7
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Lettura delle statistiche relative a riproduzione, buffering e dispositivo QOS{#read-qos-playback-buffering-and-device-statistics}

Dalla classe QOSProvider è possibile leggere le statistiche relative a riproduzione, buffering e dispositivo.

La `QOSProvider` classe fornisce diverse statistiche, tra cui informazioni sul buffering, i bit rate, i frame rate, i dati temporali e così via.

Fornisce inoltre informazioni sul dispositivo, come il produttore, il modello, il sistema operativo, la versione SDK e la dimensione/densità dello schermo.

1. Creare un&#39;istanza di un lettore multimediale.
1. Creare un `QOSProvider` oggetto e associarlo al lettore multimediale.

   ```
   // Create Media Player. 
   _mediaQosProvider = new QOSProvider; 
   _mediaQosProvider.attachMediaPlayer(_mediaPlayer);
   ```

1. (Facoltativo) Leggete le statistiche di riproduzione.

   Una soluzione per leggere le statistiche di riproduzione è avere un timer, che raccoglie periodicamente i nuovi valori QoS dal `QOSProvider`. Ad esempio:

   ```
   var qosTimer:Timer = new Timer(1000); // every 1 second  
   qosTimer.addEventListener(TimerEvent.Timer, onQoSTimer);  
   qosTimer.start(); 
   private function onQoSTimer(event:TimerEvent):void { 
       var playbackInformation:PlaybackInformation = _mediaQosProvider.getPlaybackInformation(); 
       qosInfo["Frame rate"] = playbackInformation.frameRate.toFixed();  
       qosInfo["Dropped frames"] = playbackInformation.droppedFrameCount.toFixed(); 
       qosInfo["Bitrate"] = playbackInformation.bitrate.toFixed(); 
       qosInfo["Bandwidth"] = playbackInformation.perceivedBandwidth; 
       qosInfo["Buffering time"] = playbackInformation.bufferingTime.toFixed(); 
       qosInfo["Buffer length"] = playbackInformation.bufferLength.toFixed();  
       qosInfo["Buffer time"] = playbackInformation.bufferTime.toFixed(); 
       qosInfo["Empty buffer count"] = playbackInformation.emptyBufferCount.toFixed();  
       qosInfo["Time to load"] = playbackInformation.timeToLoad.toFixed();  
       qosInfo["Time to start"] = playbackInformation.timeToStart.toFixed(); 
       qosView.update(qosInfo); 
   }
   ```

1. (Facoltativo) Leggete le informazioni specifiche del dispositivo.

   ```
   // Show device information 
   var deviceInfo:DeviceInformation = new QOSProvider.deviceInformation; 
   qosInfo["deviceModel"] = deviceInfo.manufacturer +"-" + deviceInfo.model; 
   qosInfo["os"] = deviceInfo.os;  
   qosInfo["runtime"] = deviceInfo.runtimeVersion;  
   qosInfo["widthPixels"] = deviceInfo.widthPixels;  
   qosInfo["heightPixels"] = deviceInfo.heightPixels; 
   qosView.update(qosInfo); 
   ```

