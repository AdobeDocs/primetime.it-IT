---
description: 'La versione di #EXT-X-VERSION nel file .m3u8 influenza le funzioni disponibili per l’applicazione e i tag EXT validi nella playlist/nel manifesto.'
seo-description: 'La versione di #EXT-X-VERSION nel file .m3u8 influenza le funzioni disponibili per l’applicazione e i tag EXT validi nella playlist/nel manifesto.'
seo-title: '#EXT-X-VERSION requirements'
title: '#EXT-X-VERSION requirements'
uuid: c862df4a-88ba-4497-8b7c-b83fcb34b8bb
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# #EXT-X-VERSION requirements{#ext-x-version-requirements}

La versione di #EXT-X-VERSION nel file .m3u8 influenza le funzioni disponibili per l’applicazione e i tag EXT validi nella playlist/nel manifesto.

<!--<a id="section_8850183988124049A001758F117AD3A6"></a>-->

Seguono alcune informazioni sul `#EXT-X-VERSION` tag, che specifica la versione del protocollo HLS:

* La versione deve corrispondere alle caratteristiche e agli attributi della playlist HLS; in caso contrario, potrebbero verificarsi errori di riproduzione.

   Per ulteriori informazioni, consultate [HTTP Live Streaming Specification](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1).
* La versione deve corrispondere alle caratteristiche e agli attributi della playlist HLS; in caso contrario, potrebbero verificarsi errori di riproduzione.

   Per ulteriori informazioni, consultate [HTTP Live Streaming Specification](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1).
* Adobe consiglia di utilizzare almeno la versione 2 per la riproduzione nei client basati su.

   I client e i server devono implementare le versioni nel modo seguente:

<table frame="all" colsep="1" rowsep="1" id="table_62EB98EDD9DE49EC84CB1C7D59BC40E6"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Usa almeno questa versione </th> 
   <th colname="2" class="entry"> Per utilizzare queste funzionalità </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:2 </span> </td> 
   <td colname="2"> L’attributo IV del <span class="codeph"> tag EXT-X-KEY </span> . </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:3 </span> </td> 
   <td colname="2"> 
    <ul id="ul_C9500D3F934848639C204BF248F139FF"> 
     <li id="li_535A7E3FABCB46FE872A7EA5DE2A1784">Valori di durata <span class="codeph"> EXTINF punto mobile </span> <p>I tag di durata ( <span class="codeph"> #EXTINF: Nella versione 2, </span>&lt;durata&gt;,&lt;titolo&gt; sono stati arrotondati a valori interi. La versione 3 e successive richiedono durate esatte in virgola mobile. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> <p> <span class="codeph"> EXT-X-VERSION:4 </span> </p> </td> 
   <td colname="2"> <p> 
     <ul id="ul_83D61E909D0C413FBDAB7A4A0BE1F03C"> 
      <li id="li_5071F2BE2DB74BBFB1F23B3B30C5CFD6">Il tag <span class="codeph"> EXT-X-BYTERANGE </span> </li> 
      <li id="li_A093F448567D475AB44656D4600BCBD6">Il tag <span class="codeph"> EXT-X-I-FRAME-STREAM-INF </span> </li> 
      <li id="li_1084AE3B10FD4EB387D25EEDDFBBC8CD">Il tag <span class="codeph"> EST-X-I-FRAMES-only </span> </li> 
      <li id="li_4FEFA36E300C403DBB77BB4DA46DB4EB">Il tag <span class="codeph"> EXT-X-MEDIA </span> </li> 
      <li id="li_E53D81AED45C47AEA346FA3A1B191E5C">Gli <span class="codeph"> attributi AUDIO </span> e <span class="codeph"> VIDEO </span> del tag <span class="codeph"> EXT-X-STREAM-INF </span> </li> 
      <li id="li_2E99A4971B8046F3845CF3D4D363CCCF">Audio alternativo TVSDK </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>

