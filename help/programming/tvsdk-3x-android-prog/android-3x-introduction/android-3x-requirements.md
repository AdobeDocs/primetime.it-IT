---
description: TVSDK ha requisiti specifici per contenuti multimediali, contenuti manifest, DRM e versioni software.
title: Requisiti
exl-id: 85bf7b85-5f4b-4ed5-aa4f-765dabc5d4d8
source-git-commit: 3b051c3188c81673129e12dfeb573aaf85c15c97
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 0%

---

# Requisiti {#requirements}

TVSDK ha requisiti specifici per contenuti multimediali, contenuti manifest, DRM e versioni software.

## Requisiti di sistema e software {#section_96E5B079900246E78682AE44D3F23068}

Per utilizzare TVSDK, assicurati che le versioni hardware, del sistema operativo e delle applicazioni soddisfino tutti i requisiti minimi elencati di seguito.

| Sistema operativo | Android 4.0 o successivo (livello API minimo 14) |
|---|---|
| CPU | 1 GHz Single Core o equivalente |
| RAM | 256 MB |
| GPU | GPU hardware necessaria per la riproduzione |
| Architettura | x86 tramite Houdini, ARM64, ARMv7 e ARMv8 |

## Requisiti relativi al contenuto e al manifesto {#section_72DD0E4DA9774DCCADB42887497F1386}

Controlla le restrizioni e i requisiti per i flussi e le playlist (manifesti), incluse le chiavi di crittografia DRM.

| DRM di accesso agli Adobi | Se il flusso protetto da DRM è a bit rate multiplo (MBR), la chiave di crittografia DRM utilizzata per l&#39;MBR deve essere la stessa della chiave utilizzata in tutti i flussi a bit rate. |
|---|---|
| Manifesti varianti di annunci | Deve avere le stesse rappresentazioni a bit rate delle rappresentazioni del contenuto principale. |

## #EXT-X-VERSION requisiti {#section_49A33664651A46EC9ED888BA9C1C3F6D}

Versione di `#EXT-X-VERSION` in [!DNL .m3u8] il file manifest influenza quali funzioni sono disponibili per la tua applicazione e quali `EXT` i tag sono validi.

Seguono alcune informazioni sulla `#EXT-X-VERSION` , che specifica la versione del protocollo HLS:

* La versione deve corrispondere alle caratteristiche e agli attributi della playlist HLS; in caso contrario, potrebbero verificarsi errori di riproduzione. Per ulteriori informazioni, consulta [Specifica di Streaming HTTP Live](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1).
* Adobe consiglia di utilizzare almeno la versione 2 di HLS per la riproduzione nei client basati su TVSDK.

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
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:2 </span> </td> 
   <td colname="2"> L'attributo IV del <span class="codeph"> TASTO EXT-X </span> tag . </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:3 </span> </td> 
   <td colname="2"> 
    <ul id="ul_C9500D3F934848639C204BF248F139FF"> 
     <li id="li_535A7E3FABCB46FE872A7EA5DE2A1784">Mobile-point <span class="codeph"> EXTINF </span> valori della durata <p>The duration tags ( <span class="codeph"> #EXTINF: </span>&lt;duration&gt;,&lt;title&gt;) in version 2 were rounded to integer values. La versione 3 e successive richiede che le durate siano specificate esattamente in virgola mobile. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:4 </span> </td> 
   <td colname="2"> 
    <ul id="ul_3355A6CBBE2141DDB92660BB4B604D70"> 
     <li id="li_5E73D41AF6DC4CEE88D6C029FFCFC350">La <span class="codeph"> BYTERANGE EXT-X </span> tag </li> 
     <li id="li_BF5141F516F749E5890860D487EB5287">La <span class="codeph"> EXT-X-I-FRAME-STREAM-INF </span> tag </li> 
     <li id="li_E0D399A13812499B94107CDE62998EE9">La <span class="codeph"> SOLO FOTOGRAMMI EXT-X-I </span> tag </li> 
     <li id="li_A7783AFF99854EFBBAECD2967E4CBF2B">La <span class="codeph"> EXT-X-MEDIA </span> tag </li> 
     <li id="li_15AE652F33C1454AA90DDC65E7D6C2FD">La <span class="codeph"> AUDIO </span> e <span class="codeph"> VIDEO </span> gli attributi <span class="codeph"> EXT-X-STREAM-INF </span> tag </li> 
     <li id="li_DB2A7847D5884F6E91FD9E78101FBCA5">Audio alternativo TVSDK </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>
