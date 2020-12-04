---
description: TVSDK richiede proprietà specifiche per il contenuto multimediale, il contenuto manifesto e le versioni software.
seo-description: TVSDK richiede proprietà specifiche per il contenuto multimediale, il contenuto manifesto e le versioni software.
seo-title: Requisiti
title: Requisiti
uuid: 7e5fb176-4c3f-4c12-9080-3afced28627b
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---


# Requisiti {#requirements}

TVSDK richiede proprietà specifiche per il contenuto multimediale, il contenuto manifesto e le versioni software.

## Requisiti di sistema e software {#section_61C32A0209C44230B392B113B85643EE}

Per utilizzare TVSDK, accertati che le versioni hardware, del sistema operativo e delle applicazioni soddisfino tutti i requisiti minimi elencati di seguito.

Sistema operativo: iOS 6.0 o versione successiva

## Requisiti di contenuto e manifesto {#section_05FA02E2189742008DA09D87E66DCAB7}

Controlla le limitazioni e i requisiti per flussi e playlist (manifesti), comprese le chiavi di crittografia DRM.

| Cornici chiave del segmento di contenuto | Ogni segmento di contenuto deve iniziare con un fotogramma chiave. |
|---|---|
| Numeri di sequenza in video live/lineare | Deve corrispondere a tutte le rappresentazioni con bitrate per il contenuto principale in un dato momento. |

## #EXT-X-VERSION requirements {#section_C03D3DCE1D244E26BBD2C1D7144FDFBD}

La versione di `#EXT-X-VERSION` nel file [!DNL .m3u8] influisce sulle funzioni disponibili per l&#39;applicazione e sui tag `EXT` validi nell&#39;elenco di riproduzione o nel manifesto.

Seguono alcune informazioni sul tag `#EXT-X-VERSION`, che specifica la versione del protocollo HLS:

* La versione deve corrispondere alle caratteristiche e agli attributi della playlist HLS; in caso contrario, potrebbero verificarsi errori di riproduzione.

   Per ulteriori informazioni, vedere [Specifica di streaming live HTTP](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1).
* Se il tag non è incluso nelle playlist principali o multimediali, o se non è specificata alcuna versione, per impostazione predefinita viene utilizzata la versione 1. Il contenuto non conforme alla versione 1 non verrà riprodotto.
*  Adobe consiglia di utilizzare almeno la versione 2 per la riproduzione nei client basati su TVSDK.

I client e i server devono implementare le versioni nel modo seguente:

<table id="table_62EB98EDD9DE49EC84CB1C7D59BC40E6"> 
 <thead> 
  <tr> 
   <th colname="1" class="entry"> Usa almeno questa versione </th> 
   <th colname="2" class="entry"> Per utilizzare queste funzionalità </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:2  </span> </td> 
   <td colname="2"> L'attributo IV del tag <span class="codeph"> EXT-X-KEY </span>. </td> 
  </tr> 
  <tr> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:3  </span> </td> 
   <td colname="2"> 
    <ul id="ul_C9500D3F934848639C204BF248F139FF"> 
     <li id="li_535A7E3FABCB46FE872A7EA5DE2A1784">Valori di durata <span class="codeph"> EXTINF </span> a virgola mobile <p>I tag durata ( <span class="codeph"> #EXTINF: </span>&lt;durata&gt;,&lt;titolo&gt;) nella versione 2 sono stati arrotondati a valori interi. La versione 3 e successive richiedono durate esatte in virgola mobile. </p> </li> 
     <li id="li_8DF5E91F1D5D4E19894595E1FE0A5EDE"> Funzioni TVSDK come inserimento di annunci e ABR senza soluzione di continuità </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="1"> <p> <span class="codeph"> EXT-X-VERSION:4  </span> </p> </td> 
   <td colname="2"> <p> 
     <ul id="ul_99E24D013E3141308B5A57446A9B8033"> 
      <li id="li_F36E65ADD2CA451C82FF18DBD5667927">Il tag <span class="codeph"> EXT-X-BYTERANGE </span> </li> 
      <li id="li_8C653168A7B84D11AC233E7548A8D2EF">Il tag <span class="codeph"> EXT-X-I-FRAME-STREAM-INF </span> </li> 
      <li id="li_2922B34717CB4F6189068529CDBE6D10">Il tag <span class="codeph"> EXT-X-I-FRAMES-ONLY </span> </li> 
      <li id="li_D015D78E217641D7867EB509E9F9EEE2">Il tag <span class="codeph"> EXT-X-MEDIA </span> </li> 
      <li id="li_CA068EA381984F5497FE67617CA8BB34">Gli attributi <span class="codeph"> AUDIO </span> e <span class="codeph"> VIDEO </span> del tag <span class="codeph"> EXT-X-STREAM-INF </span> </li> 
      <li id="li_EE78CC7D194A4EB2897F9AE8E4B081B8"> Audio alternativo TVSDK </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>
