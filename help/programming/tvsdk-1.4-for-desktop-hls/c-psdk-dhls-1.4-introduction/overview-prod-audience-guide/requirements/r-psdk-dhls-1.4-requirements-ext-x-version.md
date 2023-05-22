---
description: La versione di EXT-X-VERSION nel file .m3u8 influisce sulle caratteristiche disponibili per l'applicazione e sui tag EXT validi nella playlist/manifesto.
title: EXT-X-VERSION requirements
exl-id: ee778fe1-d050-4c90-af8d-6600fff72e52
source-git-commit: e2a796dc5eb017929297d127cc79b65ba51a0c75
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# EXT-X-VERSION requirements{#ext-x-version-requirements}

La versione di #EXT-X-VERSION nel file .m3u8 influisce sulle caratteristiche disponibili per l&#39;applicazione e sui tag EXT validi nella playlist/manifesto.

<!--<a id="section_8850183988124049A001758F117AD3A6"></a>-->

Seguono alcune informazioni sul tag `#EXT-X-VERSION`, che specifica la versione del protocollo HLS:

* La versione deve corrispondere alle funzioni e agli attributi nella playlist HLS; in caso contrario, potrebbero verificarsi errori di riproduzione.

   Per ulteriori informazioni, vedere [Specifiche HTTP Live Streaming](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1).
* La versione deve corrispondere alle funzioni e agli attributi nella playlist HLS; in caso contrario, potrebbero verificarsi errori di riproduzione.

   Per ulteriori informazioni, vedere [Specifiche HTTP Live Streaming](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1).
* L’Adobe consiglia di utilizzare almeno la versione 2 per la riproduzione nei client basati su.

   Client e server devono implementare le versioni nel modo seguente:

<table frame="all" colsep="1" rowsep="1" id="table_62EB98EDD9DE49EC84CB1C7D59BC40E6"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Usa almeno questa versione </th> 
   <th colname="2" class="entry"> Per utilizzare queste funzioni </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:2 </span> </td> 
   <td colname="2"> Attributo IV del tag <span class="codeph"> EXT-X-KEY </span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:3 </span> </td> 
   <td colname="2"> 
    <ul id="ul_C9500D3F934848639C204BF248F139FF"> 
     <li id="li_535A7E3FABCB46FE872A7EA5DE2A1784">Valori di durata <span class="codeph"> EXTINF a virgola mobile </span> <p>I tag di durata ( <span class="codeph"> #EXTINF: </span>&lt;durata&gt;,&lt;titolo&gt;) nella versione 2 sono stati arrotondati a valori interi. Version 3 and above require durations to be exact in floating point. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> <p> <span class="codeph"> EXT-X-VERSION:4 </span> </p> </td> 
   <td colname="2"> <p> 
     <ul id="ul_83D61E909D0C413FBDAB7A4A0BE1F03C"> 
      <li id="li_5071F2BE2DB74BBFB1F23B3B30C5CFD6">Il tag <span class="codeph"> EXT-X-BYTERANGE </span> </li> 
      <li id="li_A093F448567D475AB44656D4600BCBD6">Il tag <span class="codeph"> EXT-X-I-FRAME-STREAM-INF </span> </li> 
      <li id="li_1084AE3B10FD4EB387D25EEDDFBBC8CD">Il tag <span class="codeph"> EXT-X-I-FRAMES-ONLY </span> </li> 
      <li id="li_4FEFA36E300C403DBB77BB4DA46DB4EB">Il tag <span class="codeph"> EXT-X-MEDIA </span> </li> 
      <li id="li_E53D81AED45C47AEA346FA3A1B191E5C">Il <span class="codeph"> AUDIO </span> e <span class="codeph"> VIDEO </span> attributi di <span class="codeph"> INT-X-STREAM-INF </span> tag </li> 
      <li id="li_2E99A4971B8046F3845CF3D4D363CCCF">TVSDK alternate audio </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>
