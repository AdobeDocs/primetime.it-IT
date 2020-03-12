---
description: La classe MediaResource rappresenta il contenuto da caricare dall'istanza MediaPlayer.
seo-description: La classe MediaResource rappresenta il contenuto da caricare dall'istanza MediaPlayer.
seo-title: Creazione di una risorsa multimediale
title: Creazione di una risorsa multimediale
uuid: 3d03d92f-69b3-4da8-9b16-25a264115ae5
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# Creazione di una risorsa multimediale {#create-a-media-resource}

Per ogni nuovo contenuto video, inizializzate un’istanza MediaResource con informazioni sul contenuto video e caricate la risorsa multimediale.

La classe MediaResource rappresenta il contenuto da caricare dall&#39;istanza MediaPlayer.

1. Create un `MediaResource` passando le informazioni sul supporto al `MediaResource` costruttore.

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
      <td colname="col2"> <p>Una stringa che rappresenta l'URL del manifesto/elenco di riproduzione del file multimediale. </p> </td> 
      </tr> 
      <tr> 
      <td colname="col1"><span class="codeph"> type</span> </td> 
      <td colname="col2"> <p>Uno dei seguenti valori stringa che corrisponde al tipo di file indicato: 
        <ul id="ul_7512E90B7B294EF9BFBA2D68DE678CBB"> 
        <li id="li_AA84434E84184A3D909552794B425ABD"><span class="codeph"> MP4</span> - Formato file multimediale base ISO (MP4) </li> 
        <li id="li_8A2F3752569344B59EE30303A8393488"><span class="codeph"> HLS</span> - M3U8 </li> 
        </ul> </p> </td> 
      </tr> 
      <tr> 
      <td colname="col1"><span class="codeph"> metadata</span> </td> 
      <td colname="col2"> <p>Un'istanza della classe <span class="codeph"> Metadata</span> , che potrebbe contenere informazioni personalizzate sul contenuto da caricare. </p> <p>Esempi di contenuto sono contenuti alternativi o di annunci da inserire all'interno del contenuto principale. Se si utilizza la pubblicità, impostare <span class="codeph"> AuditudeSettings</span> prima di utilizzare questo costruttore. Per ulteriori informazioni, vedi <a href="../../../tvsdk-1.4-for-desktop-hls/ad-insertion/ad-insertion-metadata/c-psdk-dhls-1.4-ad-insertion-metadata.md" format="dita" scope="local"> Metadati</a>di inserimento annunci. </p> </td> 
      </tr> 
    </tbody> 
   </table>

   >[!IMPORTANT]
   >
   >TVSDK supporta la riproduzione solo per tipi specifici di contenuto. Se tentate di caricare qualsiasi altro tipo di contenuto, TVSDK invia un evento di errore.
   >
   >Per i contenuti video-on-demand MP4 (VOD), TVSDK non supporta la riproduzione a trucco, lo streaming ABR (Adaptive Bit Rate), l&#39;inserimento di annunci, i sottotitoli codificati o DRM.

   Il codice seguente crea un&#39; `MediaResource` istanza:

   ```
   // To do: Create metadata here
   MyResource = new MediaResource(
            "https://www.example.com/video/some-video.m3u8", 
            "HLS",
            MyMetadata)
   ```

   >[!TIP]
   >
   >A questo punto, potete utilizzare `MediaResource` accessor (getters) per esaminare il tipo, l&#39;URL e i metadati della risorsa.

1. Caricate la risorsa multimediale utilizzando una delle seguenti opzioni:

   * L’istanza di MediaPlayer.

      Per ulteriori informazioni, consultate [Caricare una risorsa multimediale in Mediaplayer](../../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/c-psdk-dhls-1.4-mediaplayer-initialize-for-video/t-psdk-dhls-1.4-media-resource-load.md).
   * A `MediaPlayerItemLoader` Per ulteriori informazioni, consultate [Caricare una risorsa multimediale in Mediaplayer](../../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/c-psdk-dhls-1.4-mediaplayer-initialize-for-video/t-psdk-dhls-1.4-media-resource-load.md).

