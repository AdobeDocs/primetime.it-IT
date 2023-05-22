---
description: La classe MediaResource rappresenta il contenuto da caricare dall'istanza MediaPlayer.
title: Creare una risorsa multimediale
exl-id: 754515e9-567d-4f9f-911d-e9dad22f71a1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---

# Creare una risorsa multimediale {#create-a-media-resource}

Per ogni nuovo contenuto video, inizializza un’istanza MediaResource con informazioni sul contenuto video e carica la risorsa multimediale.

La classe MediaResource rappresenta il contenuto da caricare dall&#39;istanza MediaPlayer.

1. Creare un `MediaResource` trasmettendo informazioni sui mezzi di comunicazione alla `MediaResource` costruttore.

   Il `MediaResource` il costruttore richiede i seguenti parametri:

   <table id="table_22886D6770FB45E99D35D0B90E6CC302">
      <thead>
      <tr>
      <th colname="col1" class="entry"> Parametro costruttore </th>
      <th colname="col2" class="entry"> Descrizione </th>
      </tr>
      </thead>
      <tbody>
      <tr>
      <td colname="col1"> <span class="codeph"> url </span> </td>
      <td colname="col2"> Stringa che rappresenta l’URL del manifesto o della playlist del file multimediale. </td>
      </tr>
      <tr>
      <td colname="col1"> <span class="codeph"> tipo </span> </td>
      <td colname="col2"> Uno dei seguenti membri della <span class="codeph"> MediaResource.Type </span> enum, corrispondente al tipo di file indicato:
      <ul id="ul_C286ED3C31364B858A1C9AF3356E9282">
      <li id="li_25B24EF76D8849DE8764539F25E435FA"> <span class="codeph"> HLS </span> - M3U8 </li>
      <li id="li_1344A41B434D49229E392F1AAF9ECA81"> <span class="codeph"> ISOBMFF </span> - Formato di file multimediale di base ISO (MP4) </li>
      <li id="li_92392073B7334916B06B16570C51AC91"> <span class="codeph"> TRATTINO </span> - MPD (MPEG-DASH MEDIA PRESENTATION description) </li>
      </ul> </td>
      </tr>
      <tr>
      <td colname="col1"> <span class="codeph"> metadati </span> </td>
      <td colname="col2"> Un'istanza di <span class="codeph"> Metadati </span> classe (una struttura simile a un dizionario), che potrebbe contenere informazioni aggiuntive sul contenuto che sta per essere caricato, ad esempio contenuto alternativo o annuncio da inserire all’interno del contenuto principale. Se utilizzi la pubblicità, imposta <span class="codeph"> AuditudeSettings </span> prima di utilizzare questo costruttore. </td>
      </tr>
      </tbody>
   </table>

   >[!IMPORTANT]
   >
   >TVSDK supporta la riproduzione solo per tipi specifici di contenuto. Se tenti di caricare un altro tipo di contenuto, TVSDK invia un evento di errore.
   >
   >Per contenuti MP4 video-on-demand (VOD), TVSDK non supporta la riproduzione con trick play, lo streaming ABR (Adaptive Bit Rate), l&#39;inserimento di annunci, i sottotitoli o DRM.

   Il codice seguente crea un `MediaResource` istanza:

   ```java
   // To do: Create metadata here
   MediaResource res = new MediaResource(
     "https://www.example.com/video/some-video.m3u8",
     MediaResource.Type.HLS,
     metadata);
   ```

   In qualsiasi momento dopo questo passaggio, puoi utilizzare `MediaResource` funzioni di accesso (getter) per esaminare il tipo, l’URL e i metadati della risorsa.

1. Carica la risorsa multimediale utilizzando una delle opzioni seguenti:

   * L’istanza MediaPlayer.
   * `MediaPlayerItemLoader` Per ulteriori informazioni, consulta [Caricare una risorsa multimediale tramite MediaPlayerItemLoader](../../../tvsdk-2.7-for-android/content-playback-options/mediaplayer-initialize-for-video/t-psdk-android-2.7-media-resource-load-using-mediaplayeritemloader.md).

   >[!IMPORTANT]
   >
   >Non caricare la risorsa multimediale su un thread in background. La maggior parte delle operazioni TVSDK deve essere eseguita sul thread principale e la loro esecuzione su un thread in background può causare la generazione di un errore e l&#39;uscita dall&#39;operazione.
