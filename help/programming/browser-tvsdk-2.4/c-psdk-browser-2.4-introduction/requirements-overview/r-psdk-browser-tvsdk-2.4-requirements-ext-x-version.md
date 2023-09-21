---
description: La versione di EXT-X-VERSION nel file .m3u8 influisce sulle funzioni disponibili per il applicazione e sui tag EXT validi nella playlist/manifesto.
title: Requisiti EXT-X-VERSION
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 0%

---

# Requisiti EXT-X-VERSION{#ext-x-version-requirements}

La versione del `#EXT-X-VERSION` file .m3u8 influisce sulle funzioni disponibili per il applicazione e sui tag EXT validi nella playlist/manifesto.

<!--<a id="section_8850183988124049A001758F117AD3A6"></a>-->

Di seguito sono riportate alcune informazioni sul `#EXT-X-VERSION` tag, che specifica la versione del protocollo HLS:

* La versione deve corrispondere alle caratteristiche e agli attributi della playlist HLS; In caso contrario, potrebbero verificarsi errori di riproduzione. Per ulteriori informazioni, vedere [Specifica HTTP](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1) Live Streaming.
* Adobe Systems consiglia di utilizzare almeno la versione 2 per la riproduzione nei client basati su Browser TVSDK.

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
   <td colname="1"> <span class="codeph"> VERSIONE EXT-X:3 </span> </td> 
   <td colname="2"> 
    <ul id="ul_C9500D3F934848639C204BF248F139FF"> 
     <li id="li_535A7E3FABCB46FE872A7EA5DE2A1784">Valori di durata EXTINF </span> a virgola <span class="codeph"> mobile <p>I tag di durata ( <span class="codeph"> #EXTINF: </span>&lt;duration&gt;,&lt;title&gt;) nella versione 2 sono stati arrotondati a valori interi. &lt;/title&gt;&lt;/duration&gt; Versione 3 e superiori richiedono che le durate siano esatte in virgola mobile. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> <span class="codeph"> VERSIONE EXT-X:4 </span> </td> 
   <td colname="2"> 
    <ul id="ul_3355A6CBBE2141DDB92660BB4B604D70"> 
     <li id="li_A7783AFF99854EFBBAECD2967E4CBF2B">Il <span class="codeph"> tag EXT-X-MEDIA </span> </li> 
     <li id="li_15AE652F33C1454AA90DDC65E7D6C2FD">Gli <span class="codeph"> attributi AUDIO </span> e <span class="codeph"> VIDEO </span> del <span class="codeph"> tag EXT-X-STREAM-INF </span> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>
