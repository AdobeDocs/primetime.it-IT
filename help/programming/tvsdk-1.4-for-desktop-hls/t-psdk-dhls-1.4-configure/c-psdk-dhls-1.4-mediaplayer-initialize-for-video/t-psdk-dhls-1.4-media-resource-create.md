---
description: La classe MediaResource rappresenta il contenuto da caricare dall'istanza MediaPlayer.
title: Creare una risorsa multimediale
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 0%

---

# Creare una risorsa multimediale {#create-a-media-resource}

Per ogni nuovo contenuto video, inizializza un’istanza MediaResource con informazioni sul contenuto video e carica la risorsa multimediale.

La classe MediaResource rappresenta il contenuto da caricare dall&#39;istanza MediaPlayer.

1. Creare un `MediaResource` trasmettendo informazioni sui mezzi di comunicazione alla `MediaResource` costruttore.

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
      <td colname="col2"> <p>Stringa che rappresenta l’URL del manifesto o della playlist del contenuto multimediale. </p> </td> 
      </tr> 
      <tr> 
      <td colname="col1"><span class="codeph"> tipo</span> </td> 
      <td colname="col2"> <p>Uno dei seguenti valori stringa che corrispondono al tipo di file indicato: 
        <ul id="ul_7512E90B7B294EF9BFBA2D68DE678CBB"> 
        <li id="li_AA84434E84184A3D909552794B425ABD"><span class="codeph"> MP4</span> - Formato di file multimediale di base ISO (MP4) </li> 
        <li id="li_8A2F3752569344B59EE30303A8393488"><span class="codeph"> HLS</span> - M3U8 </li> 
        </ul> </p> </td> 
      </tr> 
      <tr> 
      <td colname="col1"><span class="codeph"> metadati</span> </td> 
      <td colname="col2"> <p>Un'istanza di <span class="codeph"> Metadati</span> , che potrebbe contenere informazioni personalizzate sul contenuto da caricare. </p> <p>Esempi di contenuto sono il contenuto alternativo o l’annuncio da inserire all’interno del contenuto principale. Se utilizzi la pubblicità, imposta <span class="codeph"> AuditudeSettings</span> prima di utilizzare questo costruttore. Per ulteriori informazioni, consulta <a href="../../../tvsdk-1.4-for-desktop-hls/ad-insertion/ad-insertion-metadata/c-psdk-dhls-1.4-ad-insertion-metadata.md" format="dita" scope="local"> Metadati Ad Insertion</a>. </p> </td> 
      </tr> 
    </tbody> 
   </table>

   >[!IMPORTANT]
   >
   >TVSDK supporta la riproduzione solo per tipi specifici di contenuto. Se tenti di caricare un altro tipo di contenuto, TVSDK invia un evento di errore.
   >
   >Per contenuti MP4 video-on-demand (VOD), TVSDK non supporta la riproduzione con trick play, lo streaming ABR (Adaptive Bit Rate), l&#39;inserimento di annunci, i sottotitoli o DRM.

   Il codice seguente crea un `MediaResource` istanza:

   ```
   // To do: Create metadata here
   MyResource = new MediaResource(
            "https://www.example.com/video/some-video.m3u8", 
            "HLS",
            MyMetadata)
   ```

   >[!TIP]
   >
   >A questo punto, puoi utilizzare `MediaResource` funzioni di accesso (getter) per esaminare il tipo, l’URL e i metadati della risorsa.

1. Carica la risorsa multimediale utilizzando uno dei seguenti elementi:

   * Istanza MediaPlayer in uso.

     Per ulteriori informazioni, consulta [Caricare una risorsa multimediale in Mediaplayer](../../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/c-psdk-dhls-1.4-mediaplayer-initialize-for-video/t-psdk-dhls-1.4-media-resource-load.md).
   * A `MediaPlayerItemLoader` Per ulteriori informazioni, consulta [Caricare una risorsa multimediale in Mediaplayer](../../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/c-psdk-dhls-1.4-mediaplayer-initialize-for-video/t-psdk-dhls-1.4-media-resource-load.md).
