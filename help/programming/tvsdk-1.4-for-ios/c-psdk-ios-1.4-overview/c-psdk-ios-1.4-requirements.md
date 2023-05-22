---
description: TVSDK richiede proprietà specifiche per media contenuto, contenuto manifesto e versioni software.
title: Requisiti
exl-id: 2b81ae19-7907-4038-80e1-f579a8c04540
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# Requisiti {#requirements}

TVSDK richiede proprietà specifiche per il contenuto multimediale, il contenuto manifesto e le versioni software.

## Requisiti del sistema e del software {#section_61C32A0209C44230B392B113B85643EE}

Per utilizzare TVSDK, assicurati che l&#39;hardware, il sistema operativo e le versioni applicazione soddisfino tutti i requisiti minimi elencati di seguito.

Sistema operativo: iOS 6,0 o versione successiva

## Contenuto e requisiti del manifesto {#section_05FA02E2189742008DA09D87E66DCAB7}

Controlla le restrizioni e i requisiti per i flussi e le playlist (manifesti), incluse le chiavi di crittografia DRM.

| Fotogrammi chiave per segmenti di contenuto | Ogni segmento contenuto deve iniziare con un fotogramma chiave. |
|---|---|
| Numeri di sequenza in video live/lineari | Deve corrispondere in qualsiasi momento tra tutte le rappresentazioni con bitrate per il contenuto principale. |

## Requisiti #EXT-X-VERSION {#section_C03D3DCE1D244E26BBD2C1D7144FDFBD}

Versione di `#EXT-X-VERSION` nel [!DNL .m3u8] influisce sulle caratteristiche disponibili per l&#39;applicazione e sulle `EXT` I tag sono validi nella playlist/nel manifesto.

Ecco alcune informazioni sulla `#EXT-X-VERSION` tag, che specifica la versione del protocollo HLS:

* La versione deve corrispondere alle funzioni e agli attributi nella playlist HLS; in caso contrario, potrebbero verificarsi degli errori di riproduzione.

   Per ulteriori informazioni, consulta [ specifiche ](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1) per lo streaming HTTP Live.
* Se il tag non è incluso nelle playlist master o media, o se non viene specificata alcuna versione, per impostazione predefinita viene utilizzata la versione 1. Il contenuto non conforme alla versione 1 non viene riprodotto.
* Adobe Systems consiglia di utilizzare almeno la versione 2 per la riproduzione nei client basati su TVSDK.

I client e i server devono implementare le versioni nel modo seguente:

<table id="table_62EB98EDD9DE49EC84CB1C7D59BC40E6"> 
 <thead> 
  <tr> 
   <th colname="1" class="entry"> Utilizza almeno questa versione </th> 
   <th colname="2" class="entry"> Per utilizzare queste funzioni </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:2 </span> </td> 
   <td colname="2"> L'attributo IV del <span class="codeph"> TASTO EXT-X </span> tag. </td> 
  </tr> 
  <tr> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION: 3 </span> </td> 
   <td colname="2"> 
    <ul id="ul_C9500D3F934848639C204BF248F139FF"> 
     <li id="li_535A7E3FABCB46FE872A7EA5DE2A1784"><span class="codeph">Valori di durata EXTINF </span> a virgola mobile <p>I tag di durata ( <span class="codeph"> #EXTINF: </span>&lt;duration&gt;,&lt;title&gt;) nella versione 2 sono stati arrotondati ai valori interi. &lt;/title&gt;&lt;/duration&gt; Versione 3 e superiori richiedono che le durate siano esatte in virgola mobile. </p> </li> 
     <li id="li_8DF5E91F1D5D4E19894595E1FE0A5EDE"> Funzioni di TVSDK come l'inserimento annuncio e l'ABR senza interruzioni </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="1"> <p> <span class="codeph"> EXT-X-VERSION: 4 </span> </p> </td> 
   <td colname="2"> <p> 
     <ul id="ul_99E24D013E3141308B5A57446A9B8033"> 
      <li id="li_F36E65ADD2CA451C82FF18DBD5667927"><span class="codeph">Ext-X-BYTERANGE </span> tag </li> 
      <li id="li_8C653168A7B84D11AC233E7548A8D2EF"><span class="codeph">Ext-X-i-frame-Stream-INF </span> tag </li> 
      <li id="li_2922B34717CB4F6189068529CDBE6D10">Il <span class="codeph"> SOLO FRAME EXT-X-I </span> tag </li> 
      <li id="li_D015D78E217641D7867EB509E9F9EEE2">Il <span class="codeph"> EXT-X-MEDIA </span> tag </li> 
      <li id="li_CA068EA381984F5497FE67617CA8BB34">Il <span class="codeph"> AUDIO </span> e <span class="codeph"> VIDEO </span> attributi di <span class="codeph"> INT-X-STREAM-INF </span> tag </li> 
      <li id="li_EE78CC7D194A4EB2897F9AE8E4B081B8"> Audio alternativo TVSDK </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>
