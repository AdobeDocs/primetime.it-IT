---
description: Quality of Service (QoS) offre una visualizzazione dettagliata delle prestazioni del motore video. TVSDK fornisce statistiche dettagliate su riproduzione, buffering e dispositivi.
title: Statistiche sulla qualità del servizio
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 0%

---

# Statistiche sulla qualità del servizio {#quality-of-service-statistics}

Quality of Service (QoS) offre una visualizzazione dettagliata delle prestazioni del motore video. TVSDK fornisce statistiche dettagliate su riproduzione, buffering e dispositivi.

TVSDK fornisce inoltre informazioni sulle seguenti risorse scaricate:

* File playlist/manifest
* Frammenti di file
* Informazioni di tracciamento per i file

## Tracciare a livello di frammento utilizzando le informazioni di caricamento {#track-at-the-fragment-level-using-load-information}

È possibile leggere informazioni sulla qualità del servizio (QoS) relative alle risorse scaricate, ad esempio frammenti e brani, dalla classe LoadInformation.

1. Implementare `onLoadInformationAvailable` listener di eventi di callback.

   ```
   private function onLoadInformationAvailable(event:LoadInformationEvent):void { 
       var loadInformation:LoadInformation = event.loadInformation; 
       // process the load information here     
   }
   ```

1. Registra il listener di eventi, che TVSDK chiama ogni volta che un frammento è stato scaricato.

   ```
   player.addEventListener(LoadInformationEvent.LOAD_INFORMATION_AVAILABLE,  
                                    onLoadInformationAvailable);
   ```

1. Leggi i dati di interesse da `LoadInformation` che viene passato al callback.

   <table id="table_75E61A2EB25E435DB631166A7FF64757"> 
   <thead> 
   <tr> 
      <th colname="col01" class="entry"> Proprietà </th> 
      <th colname="col1" class="entry"> Tipo </th> 
      <th colname="col2" class="entry"> Descrizione </th> 
   </tr> 
   </thead>
   <tbody> 
   <tr> 
      <td colname="col01"> <span class="codeph"> downloadDuration </span> </td> 
      <td colname="col1"> <p>Numero </p> </td> 
      <td colname="col2"> <p>Durata del download in millisecondi. </p> <p>TVSDK non distingue tra il tempo impiegato dal client per connettersi al server e il tempo necessario per scaricare l’intero frammento. Ad esempio, se il download di un segmento da 10 MB richiede 8 secondi, TVSDK fornisce tali informazioni, ma non indica che sono occorsi 4 secondi prima del primo byte e altri 4 secondi per scaricare l’intero frammento. </p> </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> mediaDuration </span> </td> 
      <td colname="col1"> <p>Numero </p> </td> 
      <td colname="col2"> La durata media dei frammenti scaricati in millisecondi. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> dimensione </span> </td> 
      <td colname="col1"> <p>Numero </p> </td> 
      <td colname="col2"> Dimensione della risorsa scaricata in byte. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> trackIndex </span> </td> 
      <td colname="col1"> <p>int </p> </td> 
      <td colname="col2"> Indice del binario corrispondente, se noto; altrimenti, 0. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> trackName </span> </td> 
      <td colname="col1"> <p>Stringa </p> </td> 
      <td colname="col2"> Nome del brano corrispondente, se noto; in caso contrario, null. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> trackType </span> </td> 
      <td colname="col1"> <p>Stringa </p> </td> 
      <td colname="col2"> Tipo del brano corrispondente, se noto; altrimenti null. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> tipo </span> </td> 
      <td colname="col1"> <p>Stringa </p> </td> 
      <td colname="col2"> Informazioni scaricate da TVSDK. Uno dei seguenti elementi: 
      <ul id="ul_FA02F42D109344F4866073908CA4E835"> 
      <li id="li_0E2D3EBCAB58477FB5EA526C54FACFFB">MANIFEST (MANIFESTO): playlist/manifesto </li> 
      <li id="li_D7894C2F0CB64C909C6398288EA5683A">FRAMMENTO: un frammento </li> 
      <li id="li_4D4FEDB7704C411B80891B5028B0C20E">TRACK: frammento associato a un brano specifico </li> 
      </ul> A volte potrebbe non essere possibile rilevare il tipo di risorsa. In questo caso, viene restituito FILE. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> url </span> </td> 
      <td colname="col1"> <p>Stringa </p> </td> 
      <td colname="col2"> URL che punta alla risorsa scaricata. </td> 
   </tr> 
   </tbody> 
   </table>

## Leggi le statistiche su riproduzione, buffering e dispositivo QOS {#read-qos-playback-buffering-and-device-statistics}

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
