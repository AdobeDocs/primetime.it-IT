---
description: Dalla classe QOSProvider è possibile leggere le statistiche relative a riproduzione, buffering e dispositivo.
seo-description: Dalla classe QOSProvider è possibile leggere le statistiche relative a riproduzione, buffering e dispositivo.
seo-title: Lettura delle statistiche relative a riproduzione, buffering e dispositivo QOS
title: Lettura delle statistiche relative a riproduzione, buffering e dispositivo QOS
uuid: 19228a50-3721-4dc1-89b6-97458518e272
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 1%

---


# Leggi le statistiche relative a riproduzione, buffering e dispositivo QOS{#read-qos-playback-buffering-and-device-statistics}

Dalla classe QOSProvider è possibile leggere le statistiche relative a riproduzione, buffering e dispositivo.

La classe `QOSProvider` fornisce diverse statistiche, tra cui informazioni sul buffering, i bit rate, i frame rate, i dati temporali e così via.

Fornisce inoltre informazioni sul dispositivo, come il produttore, il modello, il sistema operativo, la versione SDK, l&#39;ID dispositivo del produttore e la dimensione/densità dello schermo.

1. Creare un&#39;istanza di un lettore multimediale.
1. Create un oggetto `QOSProvider` e collegatelo al lettore multimediale.

   Il costruttore `QOSProvider` prende il contesto di un lettore in modo che possa recuperare informazioni specifiche per il dispositivo.

   ```java
   // Create Media Player. 
   _mediaQosProvider = new QOSProvider(getActivity().getApplicationContext()); 
   _mediaQosProvider.attachMediaPlayer(_mediaPlayer);
   ```

1. (Facoltativo) Leggete le statistiche di riproduzione.

   Una soluzione per leggere le statistiche di riproduzione è avere un timer, che raccoglie periodicamente i nuovi valori QoS dal `QOSProvider`. Ad esempio:

   ```java
   _playbackClock = new Clock(PLAYBACK_CLOCK, 1000); // every 1 second 
   
   _playbackClockEventListener = new Clock.ClockEventListener() { 
       @Override 
       public void onTick(String name) { 
           getActivity().runOnUiThread(new Runnable() { 
               @Override 
               public void run() { 
                   PlaybackInformation playbackInformation = _mediaQosProvider.getPlaybackInformation();  
                   setQosItem("Frame rate", (int) playbackInformation.getFrameRate());  
                   setQosItem("Dropped frames", (int) playbackInformation.getDroppedFrameCount()); 
                   setQosItem("Bitrate", (int) playbackInformation.getBitrate()); 
                   setQosItem("Buffering time", (int) playbackInformation.getBufferingTime());  
                   setQosItem("Buffer length", (int) playbackInformation.getBufferLength());  
                   setQosItem("Buffer time", (int) playbackInformation.getBufferTime());  
                   setQosItem("Empty buffer count", (int) playbackInformation.getEmptyBufferCount());  
                   setQosItem("Time to load", (int) playbackInformation.getTimeToLoad());  
                   setQosItem("Time to start", (int) playbackInformation.getTimeToStart()); 
                   setQosItem("Time to prepare", (int) playbackInformation.getTimeToPrepare()); 
                   setQosItem("Perceived Bandwidth", (int) playbackInformation.getPerceivedBandwidth());   
                   playbackInformation.getPerceivedBandwidth()); 
               } 
           }); 
       }; 
   }; 
   ```

1. (Facoltativo) Leggete le informazioni specifiche del dispositivo.

   ```java
   // Show device information 
   DeviceInformation deviceInfo =  
     new QOSProvider(parent.getApplicationContext()).getDeviceInformation(); 
   tv = (TextView) view.findViewById(R.id.aboutDeviceModel); 
   tv.setText(parent.getString(R.string.aboutDeviceModel) + " " +  
     deviceInfo.getManufacturer() + " - " + deviceInfo.getModel()); 
   
   tv = (TextView) view.findViewById(R.id.aboutDeviceSoftware); 
   tv.setText(parent.getString(R.string.aboutDeviceSoftware) + " " +  
     deviceInfo.getOS() + ", SDK: " + deviceInfo.getSDK()); 
   
   tv = (TextView) view.findViewById(R.id.aboutDeviceResolutin); 
   String orientation = parent.getResources().getConfiguration().orientation ==  
     Configuration.ORIENTATION_LANDSCAPE ? "landscape" : "portrait"; 
   tv.setText(parent.getString(R.string.aboutDeviceResolution) + " " +  
     deviceInfo.getWidthPixels() + "x" + deviceInfo.getHeightPixels() +  
     " (" + orientation + ")"); 
   ```

