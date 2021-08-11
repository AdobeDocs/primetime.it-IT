---
description: La versione di EXT-X-VERSION nel file .m3u8 influisce sulle funzioni disponibili per la tua applicazione e sui tag EXT validi nella playlist/manifesto.
title: Requisiti della versione EXT-X
exl-id: 1b7c205b-c6b1-416f-885a-d1cd23d8e803
source-git-commit: e2a796dc5eb017929297d127cc79b65ba51a0c75
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 0%

---

# Requisiti della versione EXT-X{#ext-x-version-requirements}

La versione di `#EXT-X-VERSION` nel file .m3u8 influisce sulle funzioni disponibili per l&#39;applicazione e sui tag EXT validi nella playlist/manifesto.

<!--<a id="section_8850183988124049A001758F117AD3A6"></a>-->

Ecco alcune informazioni sul tag `#EXT-X-VERSION`, che specifica la versione del protocollo HLS:

* La versione deve corrispondere alle caratteristiche e agli attributi della playlist HLS; in caso contrario, potrebbero verificarsi errori di riproduzione. Per ulteriori informazioni, consulta [Specifica di streaming HTTP Live](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1).
* Adobe consiglia di utilizzare almeno la versione 2 per la riproduzione nei client basati su browser TVSDK.

   I client e i server devono implementare le versioni nel modo seguente:

<table frame="all" colsep="1" rowsep="1" id="table_62EB98EDD9DE49EC84CB1C7D59BC40E6"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Usa almeno questa versione </th> 
   <th colname="2" class="entry"> Per utilizzare queste funzioni </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:3  </span> </td> 
   <td colname="2"> 
    <ul id="ul_C9500D3F934848639C204BF248F139FF"> 
     <li id="li_535A7E3FABCB46FE872A7EA5DE2A1784">Valori di durata a virgola mobile <span class="codeph"> EXTINF </span> <p>Tag della durata ( <span class="codeph"> #EXTINF: </span>&lt;duration&gt;,&lt;title&gt;) nella versione 2 sono stati arrotondati a valori interi. La versione 3 e successive richiedono durate precise in virgola mobile. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:4  </span> </td> 
   <td colname="2"> 
    <ul id="ul_3355A6CBBE2141DDB92660BB4B604D70"> 
     <li id="li_A7783AFF99854EFBBAECD2967E4CBF2B">Il tag <span class="codeph"> EXT-X-MEDIA </span> </li> 
     <li id="li_15AE652F33C1454AA90DDC65E7D6C2FD">Gli attributi <span class="codeph"> AUDIO </span> e <span class="codeph"> VIDEO </span> del tag <span class="codeph"> EXT-X-STREAM-INF </span> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>
