---
description: Quality of Service (QoS) fornisce una visualizzazione dettagliata delle prestazioni del motore video. TVSDK fornisce statistiche dettagliate su riproduzione, buffering e dispositivi.
seo-description: Quality of Service (QoS) fornisce una visualizzazione dettagliata delle prestazioni del motore video. TVSDK fornisce statistiche dettagliate su riproduzione, buffering e dispositivi.
seo-title: Qualità delle statistiche di servizio
title: Qualità delle statistiche di servizio
uuid: 8e990461-065b-4efa-b77c-b2b832f86f7d
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---


# Statistiche sulla qualità del servizio {#quality-of-service-statistics}

Quality of Service (QoS) fornisce una visualizzazione dettagliata delle prestazioni del motore video. TVSDK fornisce statistiche dettagliate su riproduzione, buffering e dispositivi.

TVSDK fornisce inoltre informazioni sulle seguenti risorse scaricate:

* Sequenza di riproduzione/file manifesto
* Frammenti di file
* Informazioni di tracciamento per i file

## Tenere traccia a livello di frammento utilizzando le informazioni di caricamento {#section_4439D91E8EDC45588EF1D7BE25697350}

Dalla classe `LoadInformation` è possibile leggere informazioni sulla qualità del servizio (QoS) relative alle risorse scaricate, come frammenti e tracce.

1. Implementare e registrare il listener di eventi `MediaPlayerEvent.LOAD_INFORMATION_AVAILABLE`.
1. Chiamate `event.getLoadInformation()` per leggere i dati pertinenti dal parametro `event` passato al callback.

   >[!NOTE]
   >
   >Per ulteriori informazioni su `LoadInformation`, vedere [2.7 per i documenti API Android (Java)](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.7/index.html).

## Leggi le statistiche relative a riproduzione, buffering e dispositivo QOS {#section_D21722600F324E67A9F06234D338B243}

È possibile leggere le statistiche relative a riproduzione, buffering e dispositivo dalla classe `QOSProvider`.

La classe `QOSProvider` fornisce diverse statistiche, tra cui informazioni sul buffering, i bit rate, i frame rate, i dati temporali e così via. Fornisce inoltre informazioni sul dispositivo, come il produttore, il modello, il sistema operativo, la versione SDK, l&#39;ID dispositivo del produttore e la dimensione/densità dello schermo.

1. Creare un&#39;istanza di un lettore multimediale.
1. Create un oggetto `QOSProvider` e collegatelo al lettore multimediale.

   Il costruttore `QOSProvider` prende il contesto di un lettore in modo che possa recuperare informazioni specifiche per il dispositivo.

   ```java
   // Create Media Player. 
   _mediaQosProvider = new QOSProvider(getActivity().getApplicationContext()); 
   _mediaQosProvider.attachMediaPlayer(_mediaPlayer);
   ```

1. (Facoltativo) Leggete le statistiche di riproduzione.

   Una soluzione per leggere le statistiche di riproduzione è avere un timer, che raccoglie periodicamente i nuovi valori QoS dal `QOSProvider`.

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

1. (Facoltativo) Leggete le informazioni specifiche del dispositivo.

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

