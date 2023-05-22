---
description: TVSDK ha requisiti specifici per i contenuti multimediali, il contenuto manifesto, DRM e le versioni software.
title: Requisiti
exl-id: 8c611ad4-ad04-4bab-83b9-0d8fb6c5cf3d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---

# Requisiti {#requirements}

TVSDK ha requisiti specifici per i contenuti multimediali, il contenuto manifesto, DRM e le versioni software.

## Requisiti di sistema e software {#section_96E5B079900246E78682AE44D3F23068}

Per utilizzare TVSDK, accertati che le versioni dell&#39;hardware, del sistema operativo e delle applicazioni soddisfino tutti i requisiti minimi elencati di seguito.

| Sistema operativo | iOS 7.0 o versione successiva |
|---|---|
| Xcode | Xcode 10 per iOS 12 e Xcode 9 per iOS 11 |

## Requisiti del contenuto e del manifesto {#section_72DD0E4DA9774DCCADB42887497F1386}

Controllare le restrizioni e i requisiti per i flussi e le playlist (manifesti), incluse le chiavi di crittografia DRM.

| Fotogrammi chiave del segmento di contenuto | Ogni segmento di contenuto deve iniziare con un fotogramma chiave. |
|---|---|
| Numeri di sequenza in video live/lineari | Must match between all bit-rate renditions for the main content at any given time. |

## EXT-X-VERSION requirements {#section_C03D3DCE1D244E26BBD2C1D7144FDFBD}

La versione di `#EXT-X-VERSION` nel file manifesto di [!DNL .m3u8] influisce sulle caratteristiche disponibili per l&#39;applicazione e sui tag `EXT` validi.

Seguono alcune informazioni sul tag `#EXT-X-VERSION`, che specifica la versione del protocollo HLS:

* La versione deve corrispondere alle funzioni e agli attributi nella playlist HLS; in caso contrario, potrebbero verificarsi errori di riproduzione. Per ulteriori informazioni, vedere [Specifiche HTTP Live Streaming](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1).
* L’Adobe consiglia di utilizzare almeno la versione 2 di HLS per la riproduzione nei client basati su TVSDK.

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
   <td colname="2"> The IV attribute of the <span class="codeph"> EXT-X-KEY </span> tag. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:3 </span> </td> 
   <td colname="2"> 
    <ul id="ul_C9500D3F934848639C204BF248F139FF"> 
     <li id="li_535A7E3FABCB46FE872A7EA5DE2A1784">Valori di durata <span class="codeph"> EXTINF a virgola mobile </span> <p>I tag di durata ( <span class="codeph"> #EXTINF: </span>&lt;durata&gt;,&lt;titolo&gt;) nella versione 2 sono stati arrotondati a valori interi. La versione 3 e successive richiedono che le durate siano specificate esattamente, in virgola mobile. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:4 </span> </td> 
   <td colname="2"> 
    <ul id="ul_3355A6CBBE2141DDB92660BB4B604D70"> 
     <li id="li_5E73D41AF6DC4CEE88D6C029FFCFC350">Tag </span> EXT-X-BYTERANGE <span class="codeph"> </span></li> 
     <li id="li_BF5141F516F749E5890860D487EB5287">Il tag <span class="codeph"> EXT-X-I-FRAME-STREAM-INF </span> </li> 
     <li id="li_E0D399A13812499B94107CDE62998EE9">Il <span class="codeph"> SOLO FRAME EXT-X-I </span> tag </li> 
     <li id="li_A7783AFF99854EFBBAECD2967E4CBF2B">Il <span class="codeph"> EXT-X-MEDIA </span> tag </li> 
     <li id="li_15AE652F33C1454AA90DDC65E7D6C2FD">Il <span class="codeph"> AUDIO </span> e <span class="codeph"> VIDEO </span> attributi di <span class="codeph"> INT-X-STREAM-INF </span> tag </li> 
     <li id="li_DB2A7847D5884F6E91FD9E78101FBCA5">Audio alternativo TVSDK </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>
