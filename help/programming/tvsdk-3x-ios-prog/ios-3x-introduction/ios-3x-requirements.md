---
description: TVSDK ha requisiti specifici per le versioni media contenuto, manifest contenuto, DRM e software.
title: Requisiti
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---

# Requisiti {#requirements}

TVSDK richiede proprietà specifiche per il contenuto multimediale, il contenuto manifesto, DRM e le versioni software.

## Requisiti di sistema e software {#section_96E5B079900246E78682AE44D3F23068}

Per utilizzare TVSDK, assicurati che l&#39;hardware, il sistema operativo e le applicazione versioni soddisfino tutti i requisiti minimi elencati di seguito.

| Sistema operativo | iOS 7.0 o successivo |
|---|---|
| Xcode | Xcode 10 per iOS 12 e Xcode 9 per iOS 11 |

## Requisiti di contenuto e manifesto {#section_72DD0E4DA9774DCCADB42887497F1386}

Controllare le restrizioni e i requisiti per i flussi e le playlist (manifesti), incluse le chiavi di crittografia DRM.

| Fotogrammi chiave del segmento di contenuto | Ogni segmento di contenuto deve iniziare con un fotogramma chiave. |
|---|---|
| Numeri di sequenza in video live/lineari | In un dato momento deve corrispondere tra tutte le rappresentazioni con bitrate per il contenuto principale. |

## Requisiti EXT-X-VERSION {#section_C03D3DCE1D244E26BBD2C1D7144FDFBD}

La versione del `#EXT-X-VERSION` file manifesto [!DNL .m3u8] influisce sulle funzioni disponibili per il applicazione e sui tag `EXT` validi.

Di seguito sono riportate alcune informazioni sul `#EXT-X-VERSION` tag, che specifica la versione del protocollo HLS:

* La versione deve corrispondere alle caratteristiche e agli attributi della playlist HLS; In caso contrario, potrebbero verificarsi errori di riproduzione. Per ulteriori informazioni, vedere [Specifica HTTP](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1) Live Streaming.
* Adobe Systems consiglia di utilizzare almeno Versione 2 di HLS per la riproduzione nei client basati su TVSDK.

  I client e i server devono implementare le versioni nel modo seguente:

<table frame="all" colsep="1" rowsep="1" id="table_62EB98EDD9DE49EC84CB1C7D59BC40E6"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Utilizzare almeno questa versione </th> 
   <th colname="2" class="entry"> Per utilizzare queste funzioni </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:2 </span> </td> 
   <td colname="2"> Attributo IV del <span class="codeph"> tag EXT-X-KEY </span> . </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> VERSIONE EXT-X:3 </span> </td> 
   <td colname="2"> 
    <ul id="ul_C9500D3F934848639C204BF248F139FF"> 
     <li id="li_535A7E3FABCB46FE872A7EA5DE2A1784">Valori di durata EXTINF </span> a virgola <span class="codeph"> mobile <p>I tag di durata ( <span class="codeph"> #EXTINF: </span>&lt;duration&gt;,&lt;title&gt;) nella versione 2 sono stati arrotondati a valori interi. &lt;/title&gt;&lt;/duration&gt; Versione 3 e superiori richiedono che le durate siano specificate esattamente, in virgola mobile. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> <span class="codeph"> VERSIONE EXT-X:4 </span> </td> 
   <td colname="2"> 
    <ul id="ul_3355A6CBBE2141DDB92660BB4B604D70"> 
     <li id="li_5E73D41AF6DC4CEE88D6C029FFCFC350">Il <span class="codeph"> tag EXT-X-BYTERANGE </span> </li> 
     <li id="li_BF5141F516F749E5890860D487EB5287">Il <span class="codeph"> tag EXT-X-I-FRAME-STREAM-INF </span> </li> 
     <li id="li_E0D399A13812499B94107CDE62998EE9">Il <span class="codeph"> SOLO FRAME EXT-X-I </span> tag </li> 
     <li id="li_A7783AFF99854EFBBAECD2967E4CBF2B">Il <span class="codeph"> EXT-X-MEDIA </span> tag </li> 
     <li id="li_15AE652F33C1454AA90DDC65E7D6C2FD">Il <span class="codeph"> AUDIO </span> e <span class="codeph"> VIDEO </span> attributi di <span class="codeph"> INT-X-STREAM-INF </span> tag </li> 
     <li id="li_DB2A7847D5884F6E91FD9E78101FBCA5">Audio alternativo TVSDK </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>
