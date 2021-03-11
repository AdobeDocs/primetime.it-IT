---
description: Quality of Service (QoS) fornisce una visualizzazione dettagliata delle prestazioni del motore video. TVSDK fornisce statistiche dettagliate sulla riproduzione, il buffering e i dispositivi.
title: Qualità delle statistiche del servizio
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---


# Statistiche sulla qualità del servizio {#quality-of-service-statistics}

Quality of Service (QoS) fornisce una visualizzazione dettagliata delle prestazioni del motore video. TVSDK fornisce statistiche dettagliate sulla riproduzione, il buffering e i dispositivi.

TVSDK fornisce anche informazioni sulle seguenti risorse scaricate:

* Playlist/file manifest
* Frammenti di file
* Tracciamento delle informazioni sui file

## Tracciare a livello di frammento utilizzando le informazioni sul caricamento {#section_4439D91E8EDC45588EF1D7BE25697350}

Dalla classe `LoadInformation` è possibile leggere informazioni sulla qualità del servizio (QoS) relative alle risorse scaricate, ad esempio frammenti e tracce.

1. Implementa e registra il listener di eventi `MediaPlayerEvent.LOAD_INFORMATION_AVAILABLE`.
1. Invoca `event.getLoadInformation()` per leggere i dati pertinenti dal parametro `event` passato al callback.

   >[!NOTE]
   >
   >Per ulteriori informazioni su `LoadInformation`, consulta la sezione [2.7 per i documenti API Android (Java)](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.7/index.html).

## Leggi le statistiche relative a riproduzione, buffering e dispositivo QOS {#section_D21722600F324E67A9F06234D338B243}

È possibile leggere le statistiche di riproduzione, buffering e dispositivo dalla classe `QOSProvider` .

La classe `QOSProvider` fornisce diverse statistiche, tra cui buffering, bit rate, frame rate, dati temporali e così via. Fornisce inoltre informazioni sul dispositivo, ad esempio il produttore, il modello, il sistema operativo, la versione SDK, l&#39;ID dispositivo del produttore e la dimensione/densità dello schermo.

1. Creare un&#39;istanza di un lettore multimediale.
1. Crea un oggetto `QOSProvider` e allegalo al lettore multimediale.

   Il costruttore `QOSProvider` prende il contesto di un lettore in modo che possa recuperare informazioni specifiche per il dispositivo.

   ```java
   // Create Media Player. 
   _mediaQosProvider = new QOSProvider(getActivity().getApplicationContext()); 
   _mediaQosProvider.attachMediaPlayer(_mediaPlayer);
   ```

1. (Facoltativo) Leggere le statistiche di riproduzione.

   Una soluzione per leggere le statistiche di riproduzione è avere un timer, che recupera periodicamente i nuovi valori QoS dal `QOSProvider`.

   Ad esempio:

   ```java
   _playbackClock = new Clock(PLAYBACK_CLOCK, 1000); // every 1 second 
   _playbackClockEventListener = new Clock.ClockEventListener() { 
       @Override 
       public void onTick(String name) { 
           getActivity().runOnUiThread(new Runnable() { 
               @Override 
               public void run() { 
                   PlaybackInformation playbackInformation =  
                     _mediaQosProvider.getPlaybackInformation();  
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

1. (Facoltativo) Leggi le informazioni specifiche del dispositivo.

   ```java
   // Show device information 
   DeviceInformation deviceInfo = new QOSProvider(parent.getApplicationContext()). 
                                  getDeviceInformation(); 
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

