---
description: Quality of Service (QoS) offre una visualizzazione dettagliata delle prestazioni del motore video. TVSDK fornisce statistiche dettagliate su riproduzione, buffering e dispositivi.
seo-description: Quality of Service (QoS) offre una visualizzazione dettagliata delle prestazioni del motore video. TVSDK fornisce statistiche dettagliate su riproduzione, buffering e dispositivi.
seo-title: Qualità delle statistiche di servizio
title: Qualità delle statistiche di servizio
uuid: 5c9d09a9-0e0b-44f2-98ca-2eeb8a830ec6
translation-type: tm+mt
source-git-commit: 8ff38bdc1a7ff9732f7f1fae37f64d0e1113ff40

---


# Qualità delle statistiche di servizio {#quality-of-service-statistics}

Quality of Service (QoS) offre una visualizzazione dettagliata delle prestazioni del motore video. TVSDK fornisce statistiche dettagliate su riproduzione, buffering e dispositivi.

TVSDK fornisce inoltre informazioni sulle seguenti risorse scaricate:

* Sequenza di riproduzione/file manifesto
* Frammenti di file
* Informazioni di tracciamento per i file

## Tenere traccia a livello di frammento utilizzando le informazioni sul caricamento {#track-at-the-fragment-level-using-load-information}

Dalla classe LoadInformation è possibile leggere informazioni sulla qualità del servizio (QoS) relative alle risorse scaricate, come frammenti e tracce.

1. Implementa il listener di eventi di `onLoadInformationAvailable` callback.

   ```
   private function onLoadInformationAvailable(event:LoadInformationEvent):void { 
       var loadInformation:LoadInformation = event.loadInformation; 
       // process the load information here     
   }
   ```

1. Registra il listener di eventi, che viene chiamato da TVSDK ogni volta che un frammento viene scaricato.

   ```
   player.addEventListener(LoadInformationEvent.LOAD_INFORMATION_AVAILABLE,  
                                    onLoadInformationAvailable);
   ```

1. Leggere i dati di interesse dal callback `LoadInformation` passato.

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
      <td colname="col2"> <p>Durata del download, in millisecondi. </p> <p>TVSDK non fa distinzione tra il tempo impiegato dal client per connettersi al server e il tempo impiegato per scaricare l'intero frammento. Ad esempio, se il download di un segmento da 10 MB richiede 8 secondi, TVSDK fornisce tali informazioni, ma non indica che sono necessari 4 secondi prima del primo byte e altri 4 secondi per scaricare l’intero frammento. </p> </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> mediaDuration </span> </td> 
      <td colname="col1"> <p>Numero </p> </td> 
      <td colname="col2"> Durata media dei frammenti scaricati, in millisecondi. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> size </span> </td> 
      <td colname="col1"> <p>Numero </p> </td> 
      <td colname="col2"> La dimensione della risorsa scaricata, in byte. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> trackIndex </span> </td> 
      <td colname="col1"> <p>int </p> </td> 
      <td colname="col2"> l’indice del binario corrispondente, se noto; altrimenti, 0. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> trackName </span> </td> 
      <td colname="col1"> <p>Stringa </p> </td> 
      <td colname="col2"> il nome del binario corrispondente, se noto; altrimenti, null. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> trackType </span> </td> 
      <td colname="col1"> <p>Stringa </p> </td> 
      <td colname="col2"> il tipo del binario corrispondente, se noto; altrimenti, null. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> type </span> </td> 
      <td colname="col1"> <p>Stringa </p> </td> 
      <td colname="col2"> Download di TVSDK. Una delle seguenti opzioni: 
      <ul id="ul_FA02F42D109344F4866073908CA4E835"> 
      <li id="li_0E2D3EBCAB58477FB5EA526C54FACFFB">MANIFEST - Una playlist/un manifesto </li> 
      <li id="li_D7894C2F0CB64C909C6398288EA5683A">FRAMMENTO - Un frammento </li> 
      <li id="li_4D4FEDB7704C411B80891B5028B0C20E">TRACK - Un frammento associato a una traccia specifica </li> 
      </ul> A volte potrebbe non essere possibile rilevare il tipo di risorsa. In questo caso, viene restituito FILE. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> url </span> </td> 
      <td colname="col1"> <p>Stringa </p> </td> 
      <td colname="col2"> L’URL che fa riferimento alla risorsa scaricata. </td> 
   </tr> 
   </tbody> 
   </table>

## Lettura delle statistiche relative a riproduzione, buffering e dispositivo QOS {#read-qos-playback-buffering-and-device-statistics}

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
