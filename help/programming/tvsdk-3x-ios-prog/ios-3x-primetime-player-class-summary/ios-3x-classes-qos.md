---
description: Queste classi forniscono informazioni utili per determinare le prestazioni del lettore.
title: Classi QoS
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---


# Classi QoS {#qos-classes}

Queste classi forniscono informazioni utili per determinare le prestazioni del lettore.

<table frame="all" colsep="1" rowsep="1" id="table_2893EFF9755149159A4F94E781C76B6E"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"><b>Nome</b></th> 
   <th colname="2" class="entry"><b>Descrizione</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTDeviceInformation.html" format="html" scope="external"> PTDeviceInformation</a> </td> 
   <td colname="2">Fornisce informazioni sulla piattaforma e sul sistema operativo su cui viene eseguito il TVSDK: 
    <ul id="ul_0DE69F3B38E84964AB98DCCD11E5E123"> 
     <li id="li_19B2D1889FCA4B0F8FCB0EE8F87353B2">Versione del sistema operativo della piattaforma </li> 
     <li id="li_CA35F4A48FD34555AC7D7832D5997AD4">Numero di versione della libreria TVSDK </li> 
     <li id="li_30D38320C2A3440E92C0A477FFFBF9A0">Nome del modello del dispositivo </li> 
     <li id="li_2D15164B987E405685B96A900EBF041D">Nome del produttore del dispositivo </li> 
     <li id="li_B78485CB9580444DB9694404706BA191">UUID dispositivo </li> 
     <li id="li_841EA77499B44F0692192F9DE1A798E4">Larghezza/altezza dello schermo del dispositivo </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTPlaybackInformation.html" format="html" scope="external"> PTPlaybackInformation</a> </td> 
   <td colname="2"> Fornisce informazioni sulle prestazioni della riproduzione. Ciò include il frame rate, il bit rate del profilo, il tempo totale trascorso nel buffering, il numero di tentativi di buffering, il tempo necessario per ottenere il primo byte dal primo frammento video, il tempo necessario per eseguire il rendering del primo fotogramma, la lunghezza attualmente bufferizzata e il tempo di buffer. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTQoSProvider.html" format="html" scope="external"> PTQoSProvider</a> </td> 
   <td colname="2">
    <pre>
      Fornisce metriche QoS essenziali sia per la riproduzione che per il dispositivo.
    </pre>
    <pre>
      Classe del provider di informazioni QOS.
    </pre> </td> 
  </tr> 
 </tbody> 
</table>