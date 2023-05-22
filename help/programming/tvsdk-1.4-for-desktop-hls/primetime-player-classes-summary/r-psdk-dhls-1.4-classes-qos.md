---
description: Queste classi forniscono informazioni utili per determinare le prestazioni del lettore.
title: Classi QoS
exl-id: 7d8b2bb2-491d-4c36-a6b3-8f91cf2304aa
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 0%

---

# Classi QoS {#qos-classes}

Queste classi forniscono informazioni utili per determinare le prestazioni del lettore.

Pacchetto [com.adobe.mediacore.qos](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/package-detail.html)  Pacchetto [com.adobe.mediacore.qos.metrics](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/metrics/package-detail.html)

<table frame="all" colsep="1" rowsep="1" id="table_2893EFF9755149159A4F94E781C76B6E"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Nome </th> 
   <th colname="2" class="entry"> Descrizione </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/metrics/BufferingMetrics.html" format="html" scope="external"> BufferingMetrics</a></span> </td> 
   <td colname="2"> Fornisce informazioni sul tempo trascorso dal lettore durante il buffering e sulla frequenza con cui si è verificato un evento di buffering. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/DeviceInformation.html" format="html" scope="external"> InformazioniDispositivo</a></span> </td> 
   <td colname="2">Fornisce informazioni sulla piattaforma e sul sistema operativo su cui viene eseguito TVSDK: 
    <ul id="ul_0DE69F3B38E84964AB98DCCD11E5E123"> 
     <li id="li_19B2D1889FCA4B0F8FCB0EE8F87353B2">Versione del sistema operativo della piattaforma </li> 
     <li id="li_CA35F4A48FD34555AC7D7832D5997AD4">Numero di versione della libreria TVSDK </li> 
     <li id="li_30D38320C2A3440E92C0A477FFFBF9A0">Nome modello del dispositivo </li> 
     <li id="li_2D15164B987E405685B96A900EBF041D">Nome del produttore del dispositivo </li> 
     <li id="li_B78485CB9580444DB9694404706BA191">UUID dispositivo </li> 
     <li id="li_841EA77499B44F0692192F9DE1A798E4">Larghezza/altezza dello schermo del dispositivo </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/LoadInformation.html" format="html" scope="external"> LoadInformation</a></span> </td> 
   <td colname="2"> Contiene varie informazioni QoS sul caricamento di varie risorse (file, manifesto o playlist, frammenti/segmenti, tracce e così via). </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/LoadInformationType.html" format="html" scope="external"> LoadInformationType</a></span> </td> 
   <td colname="2"> Classe di enumerazione che elenca i valori possibili per la proprietà type degli oggetti LoadInformation. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/PlaybackInformation.html" format="html" scope="external"> PlaybackInformation</a></span> </td> 
   <td colname="2"> Fornisce informazioni sulle prestazioni della riproduzione. Ciò include il frame rate, il bit rate del profilo, il tempo totale trascorso nel buffering, il numero di tentativi di buffering, il tempo necessario per ottenere il primo byte dal primo frammento video, il tempo necessario per il rendering del primo fotogramma, la lunghezza attualmente nel buffering e il tempo del buffer. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/metrics/PlaybackLoadMetrics.html" format="html" scope="external"> PlaybackLoadMetrics</a></span> </td> 
   <td colname="2"> Fornisce informazioni sul tempo necessario al caricamento del supporto, sul tempo necessario al rendering del primo fotogramma o, in caso di errore, al mancato funzionamento del lettore. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/metrics/PlaybackMetrics.html" format="html" scope="external"> PlaybackMetrics</a></span> </td> 
   <td colname="2"> Fornisce informazioni sul comportamento della riproduzione. Ciò include la frequenza fotogrammi, la velocità bit, la lunghezza del buffer e così via. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/metrics/PlaybackSessionMetrics.html" format="html" scope="external"> PlaybackSessionMetrics</a></span> </td> 
   <td colname="2"> Fornisce informazioni sul numero di secondi trascorsi dal lettore durante la riproduzione effettiva e sul tempo effettivamente trascorso sullo schermo. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/qos/QOSProvider.html" format="html" scope="external"> QOSProvider</a></span> </td> 
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
