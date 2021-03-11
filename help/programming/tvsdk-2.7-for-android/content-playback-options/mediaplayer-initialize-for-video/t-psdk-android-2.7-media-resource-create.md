---
description: La classe MediaResource rappresenta il contenuto da caricare dall'istanza MediaPlayer.
title: Creare una risorsa multimediale
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---


# Creare una risorsa multimediale {#create-a-media-resource}

Per ogni nuovo contenuto video, inizializza un’istanza MediaResource con informazioni sul contenuto video e carica la risorsa multimediale.

La classe MediaResource rappresenta il contenuto da caricare dall&#39;istanza MediaPlayer.

1. Crea un `MediaResource` trasmettendo informazioni sui file multimediali al costruttore `MediaResource` .

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
      <td colname="col2"> Una stringa che rappresenta l'URL del manifesto/playlist del supporto. </td>
      </tr>
      <tr>
      <td colname="col1"> <span class="codeph"> type  </span> </td>
      <td colname="col2"> Uno dei seguenti membri dell'enum <span class="codeph"> MediaResource.Type </span> corrispondente al tipo di file indicato:
      <ul id="ul_C286ED3C31364B858A1C9AF3356E9282">
      <li id="li_25B24EF76D8849DE8764539F25E435FA"> <span class="codeph"> HLS  </span> - M3U8 </li>
      <li id="li_1344A41B434D49229E392F1AAF9ECA81"> <span class="codeph"> ISOBMFF  </span> - Formato del file multimediale di base ISO (MP4) </li>
      <li id="li_92392073B7334916B06B16570C51AC91"> <span class="codeph"> DASH  </span> - Descrizione della presentazione multimediale MPEG-DASH (MPD) </li>
      </ul> </td>
      </tr>
      <tr>
      <td colname="col1"> <span class="codeph"> metadati  </span> </td>
      <td colname="col2"> Un'istanza della classe <span class="codeph"> Metadati </span> (una struttura simile a un dizionario), che potrebbe contenere informazioni aggiuntive sul contenuto in fase di caricamento, ad esempio contenuto alternativo o di annunci da inserire all'interno del contenuto principale. Se utilizzi la pubblicità, imposta <span class="codeph"> AuditudeSettings </span> prima di utilizzare questo costruttore. </td>
      </tr>
      </tbody>
   </table>

   >[!IMPORTANT]
   >
   >TVSDK supporta la riproduzione solo per tipi specifici di contenuto. Se tenti di caricare qualsiasi altro tipo di contenuto, TVSDK invia un evento di errore.
   >
   >Per i contenuti video on demand MP4 (VOD), TVSDK non supporta la riproduzione a trucco, lo streaming a bit rate adattivo (ABR), l&#39;inserimento di annunci, sottotitoli o DRM.

   Il codice seguente crea un&#39;istanza `MediaResource`:

   ```java
   // To do: Create metadata here
   MediaResource res = new MediaResource(
     "https://www.example.com/video/some-video.m3u8",
     MediaResource.Type.HLS,
     metadata);
   ```

   In qualsiasi momento dopo questo passaggio, puoi utilizzare le funzioni di accesso `MediaResource` per esaminare il tipo, l’URL e i metadati della risorsa.

1. Carica la risorsa multimediale utilizzando una delle seguenti opzioni:

   * L&#39;istanza MediaPlayer.
   * `MediaPlayerItemLoader` Per ulteriori informazioni, vedere  [Caricare una risorsa multimediale utilizzando MediaPlayerItemLoader](../../../tvsdk-2.7-for-android/content-playback-options/mediaplayer-initialize-for-video/t-psdk-android-2.7-media-resource-load-using-mediaplayeritemloader.md).

   >[!IMPORTANT]
   >
   >Non caricare la risorsa multimediale su un thread in background. La maggior parte delle operazioni TVSDK devono essere eseguite sul thread principale e l&#39;esecuzione su un thread in background può causare l&#39;errore e l&#39;uscita dell&#39;operazione.
