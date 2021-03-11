---
description: È possibile leggere le statistiche di riproduzione, buffering e dispositivo dalla classe QOSProvider.
title: Leggi le statistiche relative a riproduzione, buffering e dispositivo QOS
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 1%

---


# Leggi le statistiche relative a riproduzione, buffering e dispositivo QOS{#read-qos-playback-buffering-and-device-statistics}

È possibile leggere le statistiche di riproduzione, buffering e dispositivo dalla classe QOSProvider.

La classe `QOSProvider` fornisce diverse statistiche, tra cui buffering, bit rate, frame rate, dati temporali e così via.

Fornisce inoltre informazioni sul dispositivo, ad esempio il produttore, il modello, il sistema operativo, la versione SDK e la dimensione/densità dello schermo.

1. Creare un&#39;istanza di un lettore multimediale.
1. Crea un oggetto `QOSProvider` e allegalo al lettore multimediale.

   ```
   // Create Media Player. 
   _mediaQosProvider = new QOSProvider; 
   _mediaQosProvider.attachMediaPlayer(_mediaPlayer);
   ```

1. (Facoltativo) Leggere le statistiche di riproduzione.

   Una soluzione per leggere le statistiche di riproduzione è avere un timer, che recupera periodicamente i nuovi valori QoS dal `QOSProvider`. Ad esempio:

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

1. (Facoltativo) Leggi le informazioni specifiche del dispositivo.

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

