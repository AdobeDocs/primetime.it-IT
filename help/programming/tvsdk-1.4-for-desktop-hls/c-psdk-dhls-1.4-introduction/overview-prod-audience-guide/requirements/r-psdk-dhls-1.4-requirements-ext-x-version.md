---
description: La versione di EXT-X-VERSION nel file .m3u8 influisce sulle funzioni disponibili per il applicazione e sui tag EXT validi nella playlist/manifesto.
title: Requisiti EXT-X-VERSION
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# Requisiti EXT-X-VERSION{#ext-x-version-requirements}

La versione di #EXT-X-VERSION nel file .m3u8 influisce sulle funzioni disponibili per il applicazione e sui tag EXT validi nella playlist/manifesto.

<!--<a id="section_8850183988124049A001758F117AD3A6"></a>-->

Di seguito sono riportate alcune informazioni sul `#EXT-X-VERSION` tag, che specifica la versione del protocollo HLS:

* La versione deve corrispondere alle caratteristiche e agli attributi della playlist HLS; In caso contrario, potrebbero verificarsi errori di riproduzione.

  Per ulteriori informazioni, vedere [Specifica HTTP](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1) Live Streaming.
* La versione deve corrispondere alle caratteristiche e agli attributi della playlist HLS; In caso contrario, potrebbero verificarsi errori di riproduzione.

  Per ulteriori informazioni, vedere [Specifica HTTP](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1) Live Streaming.
* Adobe Systems consiglia di utilizzare almeno la versione 2 per la riproduzione nei client basati su -.

  I client e i server devono implementare le versioni nel modo seguente:

<table frame="all" colsep="1" rowsep="1" id="table_62EB98EDD9DE49EC84CB1C7D59BC40E6"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Utilizzare almeno questa versione </th> 
   <th colname="2" class="entry"> Per utilizzare queste funzionalità </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> VERSIONE EXT-X:2 </span> </td> 
   <td colname="2"> Attributo IV del <span class="codeph"> tag EXT-X-KEY </span> . </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> VERSIONE EXT-X:3 </span> </td> 
   <td colname="2"> 
    <ul id="ul_C9500D3F934848639C204BF248F139FF"> 
     <li id="li_535A7E3FABCB46FE872A7EA5DE2A1784">Valori di durata EXTINF </span> a virgola <span class="codeph"> mobile <p>I tag di durata ( <span class="codeph"> #EXTINF: </span>&lt;duration&gt;,&lt;title&gt;) nella versione 2 sono stati arrotondati a valori interi. &lt;/title&gt;&lt;/duration&gt; Versione 3 e superiori richiedono che le durate siano esatte in virgola mobile. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> <p> <span class="codeph"> VERSIONE EXT-X:4 </span> </p> </td> 
   <td colname="2"> <p> 
     <ul id="ul_83D61E909D0C413FBDAB7A4A0BE1F03C"> 
      <li id="li_5071F2BE2DB74BBFB1F23B3B30C5CFD6">Il <span class="codeph"> tag EXT-X-BYTERANGE </span> </li> 
      <li id="li_A093F448567D475AB44656D4600BCBD6">Il <span class="codeph"> tag EXT-X-I-FRAME-STREAM-INF </span> </li> 
      <li id="li_1084AE3B10FD4EB387D25EEDDFBBC8CD">L'ESCLUSIVA <span class="codeph"> PER I FOTOGRAMMI </span> EXT-X-I tag </li> 
      <li id="li_4FEFA36E300C403DBB77BB4DA46DB4EB">Il <span class="codeph"> tag EXT-X-MEDIA </span> </li> 
      <li id="li_E53D81AED45C47AEA346FA3A1B191E5C">Il <span class="codeph"> AUDIO </span> e <span class="codeph"> VIDEO </span> attributi di <span class="codeph"> INT-X-STREAM-INF </span> tag </li> 
      <li id="li_2E99A4971B8046F3845CF3D4D363CCCF">audio alternativo TVSDK </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>
