---
description: Quality of Service (QoS) fornisce una vista dettagliata delle prestazioni del motore video. TVSDK fornisce statistiche dettagliate su riproduzione, buffering e dispositivi.
title: Statistiche sulla qualità del servizio
exl-id: 62b2b65e-7383-4694-bdec-aacc4c2ae372
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---

# Statistiche sulla qualità del servizio {#quality-of-service-statistics}

Quality of Service (QoS) fornisce una vista dettagliata delle prestazioni del motore video. TVSDK fornisce statistiche dettagliate su riproduzione, buffering e dispositivi.

TVSDK fornisce inoltre informazioni sulle seguenti risorse scaricate:

* File playlist/manifest
* Frammenti di file
* Informazioni di tracciamento per i file

## Tracciare a livello di frammento utilizzando le informazioni di caricamento {#section_4439D91E8EDC45588EF1D7BE25697350}

È possibile leggere le informazioni QoS (Quality of Service) sulle risorse scaricate, come frammenti e brani, da `LoadInformation` classe.

1. Implementare e registrare `MediaPlayerEvent.LOAD_INFORMATION_AVAILABLE` listener di eventi.
1. Chiamata `event.getLoadInformation()` per leggere i dati pertinenti dalla sezione `event` parametro passato al callback.

   >[!NOTE]
   >
   >Per ulteriori informazioni su `LoadInformation`, vedi [3.0 per Android (Java)](https://help.adobe.com/en_US/primetime/api/psdk/javadoc3.0/index.html) Documenti API.

## Leggi le statistiche su riproduzione, buffering e dispositivo QOS {#section_D21722600F324E67A9F06234D338B243}

È possibile leggere le statistiche di riproduzione, buffering e dispositivo dalla `QOSProvider` classe.

Il `QOSProvider` class fornisce varie statistiche, tra cui informazioni su buffering, bit rate, frame rate, dati temporali e così via. Fornisce inoltre informazioni sul dispositivo, ad esempio produttore, modello, sistema operativo, versione SDK, ID dispositivo del produttore e dimensioni/densità dello schermo.

1. Crea un&#39;istanza di un lettore multimediale.
1. Creare un `QOSProvider` e collegarlo al lettore multimediale.

   Il `QOSProvider` Il costruttore considera un contesto del lettore in modo da poter recuperare informazioni specifiche per il dispositivo.

   ```java
   // Create Media Player. 
   _mediaQosProvider = new QOSProvider(getActivity().getApplicationContext()); 
   _mediaQosProvider.attachMediaPlayer(_mediaPlayer);
   ```

1. (Facoltativo) Leggi le statistiche di riproduzione.

   Una soluzione per leggere le statistiche di riproduzione è disporre di un timer, che recupera periodicamente i nuovi valori QoS dalla `QOSProvider`.

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
