---
description: La classe MediaResource rappresenta il contenuto da caricare dall'istanza MediaPlayer.
seo-description: La classe MediaResource rappresenta il contenuto da caricare dall'istanza MediaPlayer.
seo-title: Creazione di una risorsa multimediale
title: Creazione di una risorsa multimediale
uuid: f34a11a3-dac2-405e-8632-1d9617cc019d
translation-type: tm+mt
source-git-commit: 1b7ec3759561159c55018b4b81f896ecc99a25e8
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 0%

---


# Creare una risorsa multimediale {#create-a-media-resource}

Per ogni nuovo contenuto video, inizializzate un’istanza MediaResource con informazioni sul contenuto video e caricate la risorsa multimediale.

La classe MediaResource rappresenta il contenuto da caricare dall&#39;istanza MediaPlayer.

1. Creare un `MediaResource` trasmettendo informazioni sul supporto al costruttore `MediaResource`.

   Il costruttore `MediaResource` richiede i seguenti parametri:

   <table id="table_22886D6770FB45E99D35D0B90E6CC302">
      <thead>
      <tr>
      <th colname="col1" class="entry"> Parametro costruttore </th>
      <th colname="col2" class="entry"> Descrizione </th>
      </tr>
      </thead>
      <tbody>
      <tr>
      <td colname="col1"> <span class="codeph"> url  </span> </td>
      <td colname="col2"> Una stringa che rappresenta l'URL del manifesto/elenco di riproduzione del file multimediale. </td>
      </tr>
      <tr>
      <td colname="col1"> <span class="codeph"> type  </span> </td>
      <td colname="col2"> Uno dei seguenti membri dell'enum <span class="codeph"> MediaResource.Type </span>, corrispondente al tipo di file indicato:
      <ul id="ul_C286ED3C31364B858A1C9AF3356E9282">
      <li id="li_25B24EF76D8849DE8764539F25E435FA"> <span class="codeph"> HLS  </span> - M3U8 </li>
      <li id="li_1344A41B434D49229E392F1AAF9ECA81"> <span class="codeph"> ISOBMFF  </span> - Formato file multimediale di base ISO (MP4) </li>
      <li id="li_92392073B7334916B06B16570C51AC91"> <span class="codeph"> DASH  </span> - Descrizione della presentazione multimediale MPEG-DASH (MPD) </li>
      </ul> </td>
      </tr>
      <tr>
      <td colname="col1"> <span class="codeph"> metadata  </span> </td>
      <td colname="col2"> Un'istanza della classe <span class="codeph"> Metadata </span> (una struttura di tipo dizionario), che potrebbe contenere informazioni aggiuntive sul contenuto che sta per essere caricato, ad esempio contenuto alternativo o contenuto annuncio da inserire all'interno del contenuto principale. Se si utilizza la pubblicità, impostare <span class="codeph"> AuditudeSettings </span> prima di utilizzare questo costruttore. </td>
      </tr>
      </tbody>
   </table>

   >[!IMPORTANT]
   >
   >TVSDK supporta la riproduzione solo per tipi specifici di contenuto. Se tentate di caricare qualsiasi altro tipo di contenuto, TVSDK invia un evento di errore.
   >
   >Per i contenuti video on-demand MP4 (VOD), TVSDK non supporta la riproduzione a trucco, lo streaming ABR (Adaptive Bit Rate), l&#39;inserimento di annunci, i sottotitoli codificati o DRM.

   Il codice seguente crea un&#39;istanza `MediaResource`:

   ```java
   // To do: Create metadata here
   MediaResource res = new MediaResource(
     "https://www.example.com/video/some-video.m3u8",
     MediaResource.Type.HLS,
     metadata);
   ```

   In qualsiasi momento dopo questo passaggio, potete utilizzare gli accessori `MediaResource` (getters) per esaminare il tipo, l&#39;URL e i metadati della risorsa.

1. Caricate la risorsa multimediale utilizzando una delle seguenti opzioni:

   * L’istanza MediaPlayer.
   * `MediaPlayerItemLoader` Per ulteriori informazioni, consultate  [Caricare una risorsa multimediale utilizzando MediaPlayerItemLoader](../../../tvsdk-2.7-for-android/content-playback-options/mediaplayer-initialize-for-video/t-psdk-android-2.7-media-resource-load-using-mediaplayeritemloader.md).

   >[!IMPORTANT]
   >
   >Non caricate la risorsa multimediale su un thread in background. La maggior parte delle operazioni TVSDK devono essere eseguite sul thread principale e l&#39;esecuzione di tali operazioni su un thread in background può causare l&#39;errore e l&#39;uscita dall&#39;operazione.
