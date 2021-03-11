---
description: È possibile leggere informazioni sulla qualità del servizio (QoS) relative alle risorse scaricate, ad esempio frammenti e tracce, dalla classe LoadInformation.
title: Tracciare a livello di frammento utilizzando le informazioni sul caricamento
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---


# Tracciare a livello di frammento utilizzando le informazioni sul caricamento{#track-at-the-fragment-level-using-load-information}

È possibile leggere informazioni sulla qualità del servizio (QoS) relative alle risorse scaricate, ad esempio frammenti e tracce, dalla classe LoadInformation.

1. Implementa il listener di eventi di callback `onLoadInformationAvailable` .

   ```
   private function onLoadInformationAvailable(event:LoadInformationEvent):void { 
       var loadInformation:LoadInformation = event.loadInformation; 
       // process the load information here     
   }
   ```

1. Registra il listener di eventi, che TVSDK chiama ogni volta che un frammento viene scaricato.

   ```
   player.addEventListener(LoadInformationEvent.LOAD_INFORMATION_AVAILABLE,  
                                    onLoadInformationAvailable);
   ```

1. Leggi i dati di interesse del `LoadInformation` passato al callback.

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
      <td colname="col01"> <span class="codeph"> downloadDuration  </span> </td> 
      <td colname="col1"> <p>Numero </p> </td> 
      <td colname="col2"> <p>Durata del download in millisecondi. </p> <p>TVSDK non distingue tra il tempo impiegato dal client per connettersi al server e il tempo impiegato per scaricare l’intero frammento. Ad esempio, se il download di un segmento da 10 MB richiede 8 secondi, TVSDK fornisce tali informazioni, ma non indica che sono necessari 4 secondi fino al primo byte e altri 4 secondi per scaricare l’intero frammento. </p> </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> mediaDuration  </span> </td> 
      <td colname="col1"> <p>Numero </p> </td> 
      <td colname="col2"> Durata dei frammenti scaricati in millisecondi. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> size  </span> </td> 
      <td colname="col1"> <p>Numero </p> </td> 
      <td colname="col2"> Dimensione della risorsa scaricata in byte. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> trackIndex  </span> </td> 
      <td colname="col1"> <p>int </p> </td> 
      <td colname="col2"> l'indice del binario corrispondente, se noto; altrimenti, 0. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> trackName  </span> </td> 
      <td colname="col1"> <p>Stringa </p> </td> 
      <td colname="col2"> il nome del brano corrispondente, se noto; altrimenti, null. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> trackType  </span> </td> 
      <td colname="col1"> <p>Stringa </p> </td> 
      <td colname="col2"> il tipo di binario corrispondente, se noto; altrimenti, null. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> type  </span> </td> 
      <td colname="col1"> <p>Stringa </p> </td> 
      <td colname="col2"> Cos’è stato scaricato TVSDK. Una delle seguenti opzioni: 
      <ul id="ul_FA02F42D109344F4866073908CA4E835"> 
      <li id="li_0E2D3EBCAB58477FB5EA526C54FACFFB">MANIFEST - Una playlist/manifesto </li> 
      <li id="li_D7894C2F0CB64C909C6398288EA5683A">FRAMMENTO - Un frammento </li> 
      <li id="li_4D4FEDB7704C411B80891B5028B0C20E">TRACK - Un frammento associato a una traccia specifica </li> 
      </ul> A volte potrebbe non essere possibile rilevare il tipo di risorsa. In questo caso, viene restituito FILE. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> url  </span> </td> 
      <td colname="col1"> <p>Stringa </p> </td> 
      <td colname="col2"> URL che punta alla risorsa scaricata. </td> 
   </tr> 
   </tbody> 
   </table>
