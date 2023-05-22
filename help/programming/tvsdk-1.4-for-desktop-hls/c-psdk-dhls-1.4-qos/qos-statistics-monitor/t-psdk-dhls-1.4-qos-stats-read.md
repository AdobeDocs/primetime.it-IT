---
description: È possibile leggere le statistiche di riproduzione, buffering e dispositivo dalla classe QOSProvider.
title: Leggi le statistiche su riproduzione, buffering e dispositivo QOS
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---


# Leggi le statistiche su riproduzione, buffering e dispositivo QOS{#read-qos-playback-buffering-and-device-statistics}

È possibile leggere le statistiche di riproduzione, buffering e dispositivo dalla classe QOSProvider.

Il `QOSProvider` class fornisce varie statistiche, tra cui informazioni su buffering, bit rate, frame rate, dati temporali e così via.

Fornisce inoltre informazioni sul dispositivo, ad esempio produttore, modello, sistema operativo, versione SDK e dimensioni/densità dello schermo.

1. Crea un&#39;istanza di un lettore multimediale.
1. Creare un `QOSProvider` e collegarlo al lettore multimediale.

   ```
   // Create Media Player. 
   _mediaQosProvider = new QOSProvider; 
   _mediaQosProvider.attachMediaPlayer(_mediaPlayer);
   ```

1. (Facoltativo) Leggi le statistiche di riproduzione.

   Una soluzione per leggere le statistiche di riproduzione è disporre di un timer, che recupera periodicamente i nuovi valori QoS dalla `QOSProvider`. Ad esempio:

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

