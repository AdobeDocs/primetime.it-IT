---
description: TVSDK richiede requisiti specifici per media contenuto, contenuto manifest, DRM e versioni software.
title: Requisiti
exl-id: 8fafc52e-01b5-448f-a235-7bc3a72f4d80
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 0%

---

# Requisiti {#requirements}

TVSDK richiede requisiti specifici per media contenuto, contenuto manifest, DRM e versioni software.

## Requisiti di sistema e software {#section_96E5B079900246E78682AE44D3F23068}

Per utilizzare TVSDK, accertati che le versioni dell&#39;hardware, del sistema operativo e delle applicazioni soddisfino tutti i requisiti minimi elencati di seguito.

| Sistema operativo | Android 4.0 o versione successiva (livello minimo API 14) |
|---|---|
| CPU | 1 GHz single-core o equivalente |
| RAM | 256 MB |
| GPU | GPU hardware necessaria per la riproduzione |
| Architettura | x86 tramite Houdini, ARM64, ARMv7 e ARMv8 |

## Requisiti del contenuto e del manifesto {#section_72DD0E4DA9774DCCADB42887497F1386}

Controllare le restrizioni e i requisiti per i flussi e le playlist (manifesti), incluse le chiavi di crittografia DRM.

| DRM accesso Adobe | Se il flusso protetto da DRM è a velocità bit multipla (MBR), la chiave di crittografia DRM utilizzata per l&#39;MBR deve essere la stessa della chiave utilizzata in tutti i flussi di velocità bit. |
|---|---|
| Manifesti della variante dell’annuncio | Devono avere le stesse rappresentazioni di bitrate come le rappresentazioni del contenuto principale. |

## #EXT-X-requisiti di versione {#section_49A33664651A46EC9ED888BA9C1C3F6D}

La versione di `#EXT-X-VERSION` nel [!DNL .m3u8] file influisce sulle funzioni disponibili per il applicazione e `EXT` sui tag validi nella playlist/manifesto.

Ecco alcune informazioni sulla `#EXT-X-VERSION` tag, che specifica la versione del protocollo HLS:

* La versione deve corrispondere alle funzioni e agli attributi nella playlist HLS; in caso contrario, potrebbero verificarsi degli errori di riproduzione. Per ulteriori informazioni, consulta [Specifiche di HTTP Live Streaming](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1).
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
   <td colname="1"> <span class="codeph"> EXT-X-VERSION: 2 </span> </td> 
   <td colname="2"> L'attributo IV del <span class="codeph"> TASTO EXT-X </span> tag. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION: 3 </span> </td> 
   <td colname="2"> 
    <ul id="ul_C9500D3F934848639C204BF248F139FF"> 
     <li id="li_535A7E3FABCB46FE872A7EA5DE2A1784"><span class="codeph">Valori di durata EXTINF </span> a virgola mobile <p>I tag di durata ( <span class="codeph"> #EXTINF: </span>&lt;duration&gt;,&lt;title&gt;) nella versione 2 sono stati arrotondati ai valori interi. &lt;/title&gt;&lt;/duration&gt; Versione 3 e superiori richiedono che le durate siano specificate esattamente, in virgola mobile. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION: 4 </span> </td> 
   <td colname="2"> 
    <ul id="ul_3355A6CBBE2141DDB92660BB4B604D70"> 
     <li id="li_5E73D41AF6DC4CEE88D6C029FFCFC350">Il <span class="codeph"> INT-X-BYTERANGE </span> tag </li> 
     <li id="li_BF5141F516F749E5890860D487EB5287">Il <span class="codeph"> EXT-X-I-FRAME-STREAM-INF </span> tag </li> 
     <li id="li_E0D399A13812499B94107CDE62998EE9">Il <span class="codeph"> SOLO FRAME EXT-X-I </span> tag </li> 
     <li id="li_A7783AFF99854EFBBAECD2967E4CBF2B">Il <span class="codeph"> EXT-X-MEDIA </span> tag </li> 
     <li id="li_15AE652F33C1454AA90DDC65E7D6C2FD">Il <span class="codeph"> AUDIO </span> e <span class="codeph"> VIDEO </span> attributi di <span class="codeph"> INT-X-STREAM-INF </span> tag </li> 
     <li id="li_DB2A7847D5884F6E91FD9E78101FBCA5">Audio alternativo TVSDK </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>
