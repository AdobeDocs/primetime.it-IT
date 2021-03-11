---
description: La classe MediaResource rappresenta il contenuto da caricare dall'istanza MediaPlayer.
title: Creare una risorsa multimediale
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 0%

---


# Creare una risorsa multimediale {#create-a-media-resource}

Per ogni nuovo contenuto video, inizializza un’istanza MediaResource con informazioni sul contenuto video e carica la risorsa multimediale.

La classe MediaResource rappresenta il contenuto da caricare dall&#39;istanza MediaPlayer.

1. Crea un `MediaResource` trasmettendo informazioni sui file multimediali al costruttore `MediaResource` .

   <table id="table_DD0D5D9129D54F73881399B9B4FF546A"> 
    <thead> 
      <tr> 
      <th colname="col1" class="entry"> Parametro costruttore </th> 
      <th colname="col2" class="entry"> Descrizione </th> 
      </tr>
    </thead>
    =<tbody> 
      <tr> 
      <td colname="col1"><span class="codeph"> url</span> </td> 
      <td colname="col2"> <p>Una stringa che rappresenta l'URL del manifesto/playlist del file multimediale. </p> </td> 
      </tr> 
      <tr> 
      <td colname="col1"><span class="codeph"> type</span> </td> 
      <td colname="col2"> <p>Uno dei seguenti valori stringa che corrisponde al tipo di file indicato: 
        <ul id="ul_7512E90B7B294EF9BFBA2D68DE678CBB"> 
        <li id="li_AA84434E84184A3D909552794B425ABD"><span class="codeph"> MP4</span>  - Formato del file multimediale di base ISO (MP4) </li> 
        <li id="li_8A2F3752569344B59EE30303A8393488"><span class="codeph"> HLS</span>  - M3U8 </li> 
        </ul> </p> </td> 
      </tr> 
      <tr> 
      <td colname="col1"><span class="codeph"> metadati</span> </td> 
      <td colname="col2"> <p>Un'istanza della classe <span class="codeph"> Metadata</span> che potrebbe contenere informazioni personalizzate sul contenuto da caricare. </p> <p>Esempi di contenuto sono contenuti alternativi o di annunci da inserire all’interno del contenuto principale. Se utilizzi la pubblicità, imposta <span class="codeph"> AuditudeSettings</span> prima di utilizzare questo costruttore. Per ulteriori informazioni, consulta <a href="../../../tvsdk-1.4-for-desktop-hls/ad-insertion/ad-insertion-metadata/c-psdk-dhls-1.4-ad-insertion-metadata.md" format="dita" scope="local"> Metadati Ad Insertion</a>. </p> </td> 
      </tr> 
    </tbody> 
   </table>

   >[!IMPORTANT]
   >
   >TVSDK supporta la riproduzione solo per tipi specifici di contenuto. Se tenti di caricare qualsiasi altro tipo di contenuto, TVSDK invia un evento di errore.
   >
   >Per i contenuti video on demand MP4 (VOD), TVSDK non supporta la riproduzione a trucco, lo streaming a bit rate adattivo (ABR), l&#39;inserimento di annunci, sottotitoli o DRM.

   Il codice seguente crea un&#39;istanza `MediaResource`:

   ```
   // To do: Create metadata here
   MyResource = new MediaResource(
            "https://www.example.com/video/some-video.m3u8", 
            "HLS",
            MyMetadata)
   ```

   >[!TIP]
   >
   >A questo punto, puoi utilizzare le funzioni di accesso `MediaResource` per esaminare il tipo, l’URL e i metadati della risorsa.

1. Carica la risorsa multimediale utilizzando uno dei seguenti elementi:

   * L&#39;istanza MediaPlayer.

      Per ulteriori informazioni, consulta [Caricare una risorsa multimediale in Mediaplayer](../../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/c-psdk-dhls-1.4-mediaplayer-initialize-for-video/t-psdk-dhls-1.4-media-resource-load.md).
   * A `MediaPlayerItemLoader` Per ulteriori informazioni, vedere [Caricare una risorsa multimediale in Mediaplayer](../../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/c-psdk-dhls-1.4-mediaplayer-initialize-for-video/t-psdk-dhls-1.4-media-resource-load.md).

