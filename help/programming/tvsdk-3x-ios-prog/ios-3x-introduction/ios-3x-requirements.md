---
description: TVSDK ha requisiti specifici per contenuti multimediali, contenuti manifest, DRM e versioni software.
seo-description: TVSDK ha requisiti specifici per contenuti multimediali, contenuti manifest, DRM e versioni software.
seo-title: Requisiti
title: Requisiti
uuid: 06e61b9f-cda2-4813-8da4-fb3e0d88ad35
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# Requisiti {#requirements}

TVSDK richiede proprietà specifiche per contenuti multimediali, contenuti manifest, DRM e versioni software.

## Requisiti di sistema e software {#section_96E5B079900246E78682AE44D3F23068}

Per utilizzare TVSDK, accertati che le versioni hardware, del sistema operativo e delle applicazioni soddisfino tutti i requisiti minimi elencati di seguito.

| Sistema operativo | iOS 7.0 o successivo |
|---|---|
| Xcode | Xcode 10 per iOS 12 e Xcode 9 per iOS 11 |

## Requisiti di contenuto e manifesto {#section_72DD0E4DA9774DCCADB42887497F1386}

Controlla le limitazioni e i requisiti per flussi e playlist (manifesti), comprese le chiavi di crittografia DRM.

| Cornici chiave del segmento di contenuto | Ogni segmento di contenuto deve iniziare con un fotogramma chiave. |
|---|---|
| Numeri di sequenza in video live/lineare | Deve corrispondere a tutte le rappresentazioni con bitrate per il contenuto principale in un dato momento. |

## Requisiti della versione EXT-X {#section_C03D3DCE1D244E26BBD2C1D7144FDFBD}

La versione del file `#EXT-X-VERSION` del [!DNL .m3u8] manifesto influisce sulle funzioni disponibili per l&#39;applicazione e sui `EXT` tag validi.

Seguono alcune informazioni sul `#EXT-X-VERSION` tag, che specifica la versione del protocollo HLS:

* La versione deve corrispondere alle caratteristiche e agli attributi della playlist HLS; in caso contrario, potrebbero verificarsi errori di riproduzione. Per ulteriori informazioni, consultate [HTTP Live Streaming Specification](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1).
* Adobe consiglia di utilizzare almeno la versione 2 di HLS per la riproduzione nei client basati su TVSDK.

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
     <li id="li_535A7E3FABCB46FE872A7EA5DE2A1784">Valori di durata <span class="codeph"> EXTINF punto mobile </span> <p>I tag di durata ( <span class="codeph"> #EXTINF: Nella versione 2, </span>&lt;durata&gt;,&lt;titolo&gt; sono stati arrotondati a valori interi. La versione 3 e successive richiedono che le durate siano specificate esattamente, in virgola mobile. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:4 </span> </td> 
   <td colname="2"> 
    <ul id="ul_3355A6CBBE2141DDB92660BB4B604D70"> 
     <li id="li_5E73D41AF6DC4CEE88D6C029FFCFC350">Il tag <span class="codeph"> EXT-X-BYTERANGE </span> </li> 
     <li id="li_BF5141F516F749E5890860D487EB5287">Il tag <span class="codeph"> EXT-X-I-FRAME-STREAM-INF </span> </li> 
     <li id="li_E0D399A13812499B94107CDE62998EE9">Il tag <span class="codeph"> EST-X-I-FRAMES-only </span> </li> 
     <li id="li_A7783AFF99854EFBBAECD2967E4CBF2B">Il tag <span class="codeph"> EXT-X-MEDIA </span> </li> 
     <li id="li_15AE652F33C1454AA90DDC65E7D6C2FD">Gli <span class="codeph"> attributi AUDIO </span> e <span class="codeph"> VIDEO </span> del tag <span class="codeph"> EXT-X-STREAM-INF </span> </li> 
     <li id="li_DB2A7847D5884F6E91FD9E78101FBCA5">Audio alternativo TVSDK </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>