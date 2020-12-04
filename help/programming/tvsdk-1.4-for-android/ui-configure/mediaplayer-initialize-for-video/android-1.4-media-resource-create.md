---
description: Per ogni nuovo contenuto video, inizializzate un’istanza MediaResource con informazioni sul contenuto video e caricate la risorsa multimediale. La classe MediaResource rappresenta il contenuto da caricare dall'istanza MediaPlayer.
seo-description: Per ogni nuovo contenuto video, inizializzate un’istanza MediaResource con informazioni sul contenuto video e caricate la risorsa multimediale. La classe MediaResource rappresenta il contenuto da caricare dall'istanza MediaPlayer.
seo-title: Creazione di una risorsa multimediale
title: Creazione di una risorsa multimediale
uuid: d9fe982a-bedf-445c-b5be-f7918693782a
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 0%

---


# Creare una risorsa multimediale {#create-a-media-resource}

Per ogni nuovo contenuto video, inizializzate un’istanza MediaResource con informazioni sul contenuto video e caricate la risorsa multimediale. La classe MediaResource rappresenta il contenuto da caricare dall&#39;istanza MediaPlayer.

1. Creare un `MediaResource` trasmettendo informazioni sul supporto al costruttore `MediaResource`.

   <table id="table_DD0D5D9129D54F73881399B9B4FF546A"> 
    <thead> 
    <tr> 
    <th colname="col1" class="entry"> Parametro costruttore </th> 
    <th colname="col2" class="entry"> Descrizione </th> 
    </tr> 
    </thead>
    <tbody> 
    <tr> 
    <td colname="col1"> <p>url </p> </td> 
    <td colname="col2"> <p>Una stringa che rappresenta l'URL del manifesto/elenco di riproduzione del file multimediale. </p> </td> 
    </tr> 
    <tr> 
    <td colname="col1"> <p>type </p> </td> 
    <td colname="col2"> <p>Uno dei seguenti membri dell'enumerazione <span class="codeph"> MediaResource.Type </span> che corrisponde al tipo di file indicato: 
    <ul id="ul_72636C41CA7E4538A3BE11A79E0282FC"> 
    <li id="li_070960200DEB40E992C58FCB8909AEA3"> <span class="codeph"> HLS  </span> - M3U8 </li> 
    </ul> </p> </td> 
    </tr> 
    <tr> 
    <td colname="col1"> <p>metadata </p> </td> 
    <td colname="col2"> <p>Un'istanza della classe <span class="codeph"> Metadata </span>, che potrebbe contenere informazioni personalizzate sul contenuto da caricare. </p> <p>Esempi di contenuto sono contenuti alternativi o di annunci da inserire all'interno del contenuto principale. Se si utilizza la pubblicità, impostare <span class="codeph"> AuditudeSettings </span>. Per ulteriori informazioni, vedere <a href="../../../tvsdk-1.4-for-android/ad-insertion/ad-insertion-metadata/android-1.4-ad-insertion-metadata-set-up.md" format="dita" scope="local">  Ad Insertion Metadata </a>. </p> </td> 
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
   try { 
       // create a MediaResource instance pointing to some HLS content 
       Metadata metadata = //TODO: create metadata  
       MediaResource mediaResource = MediaResource.createFromUrl( 
         "https://www.example.com/video/some-video.m3u8",  
         MediaResource.Type.HLS,  
         metadata); 
   } catch(IllegalArgumentException ex) { 
       // this exception is thrown if the URL does not point  
       // to a valid url. 
   } 
   ```

   >[!TIP]
   >
   >A questo punto, è possibile utilizzare gli accessori `MediaResource` (getters) per esaminare il tipo di risorsa, l&#39;URL e i metadati.

1. Caricate la risorsa multimediale utilizzando quanto segue:

   * L’istanza di MediaPlayer.

      Per ulteriori informazioni, vedere [Caricare una risorsa multimediale in MediaPlayer](../../../tvsdk-1.4-for-android/ui-configure/mediaplayer-initialize-for-video/android-1.4-media-resource-load.md).
   * A `MediaPlayerItemLoader` Per ulteriori informazioni, vedere [Caricare una risorsa multimediale utilizzando MediaPlayerItemLoader](../../../tvsdk-1.4-for-android/ui-configure/mediaplayer-initialize-for-video/android-1.4-media-mediaplayeritemloader.md).
   >[!IMPORTANT]
   >
   >Non caricate la risorsa multimediale su un thread in background. La maggior parte delle operazioni TVSDK devono essere eseguite sul thread principale e l&#39;esecuzione di tali operazioni su un thread in background può causare l&#39;errore e l&#39;uscita dall&#39;operazione.
