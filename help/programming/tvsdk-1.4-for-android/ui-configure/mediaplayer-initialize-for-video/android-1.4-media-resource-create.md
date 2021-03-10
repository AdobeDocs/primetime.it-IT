---
description: Per ogni nuovo contenuto video, inizializza un’istanza MediaResource con informazioni sul contenuto video e carica la risorsa multimediale. La classe MediaResource rappresenta il contenuto da caricare dall'istanza MediaPlayer.
title: Creare una risorsa multimediale
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---


# Creare una risorsa multimediale {#create-a-media-resource}

Per ogni nuovo contenuto video, inizializza un’istanza MediaResource con informazioni sul contenuto video e carica la risorsa multimediale. La classe MediaResource rappresenta il contenuto da caricare dall&#39;istanza MediaPlayer.

1. Crea un `MediaResource` trasmettendo informazioni sui file multimediali al costruttore `MediaResource` .

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
    <td colname="col2"> <p>Una stringa che rappresenta l'URL del manifesto/playlist del file multimediale. </p> </td> 
    </tr> 
    <tr> 
    <td colname="col1"> <p>type </p> </td> 
    <td colname="col2"> <p>Uno dei seguenti membri dell'enumerazione <span class="codeph"> MediaResource.Type </span> che corrisponde al tipo di file indicato: 
    <ul id="ul_72636C41CA7E4538A3BE11A79E0282FC"> 
    <li id="li_070960200DEB40E992C58FCB8909AEA3"> <span class="codeph"> HLS  </span> - M3U8 </li> 
    </ul> </p> </td> 
    </tr> 
    <tr> 
    <td colname="col1"> <p>metadati </p> </td> 
    <td colname="col2"> <p>Un'istanza della classe <span class="codeph"> Metadata </span> che potrebbe contenere informazioni personalizzate sul contenuto da caricare. </p> <p>Esempi di contenuto sono contenuti alternativi o di annunci da inserire all’interno del contenuto principale. Se utilizzi la pubblicità, imposta <span class="codeph"> AuditudeSettings </span>. Per ulteriori informazioni, consulta <a href="../../../tvsdk-1.4-for-android/ad-insertion/ad-insertion-metadata/android-1.4-ad-insertion-metadata-set-up.md" format="dita" scope="local"> Metadati Ad Insertion </a>. </p> </td> 
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
   >A questo punto, puoi utilizzare le funzioni di accesso `MediaResource` per esaminare il tipo, l’URL e i metadati della risorsa.

1. Carica la risorsa multimediale utilizzando quanto segue:

   * L&#39;istanza MediaPlayer.

      Per ulteriori informazioni, consulta [Caricare una risorsa multimediale in MediaPlayer](../../../tvsdk-1.4-for-android/ui-configure/mediaplayer-initialize-for-video/android-1.4-media-resource-load.md).
   * A `MediaPlayerItemLoader` Per ulteriori informazioni, vedere [Caricare una risorsa multimediale utilizzando MediaPlayerItemLoader](../../../tvsdk-1.4-for-android/ui-configure/mediaplayer-initialize-for-video/android-1.4-media-mediaplayeritemloader.md).
   >[!IMPORTANT]
   >
   >Non caricare la risorsa multimediale su un thread in background. La maggior parte delle operazioni TVSDK devono essere eseguite sul thread principale e l&#39;esecuzione su un thread in background può causare l&#39;errore e l&#39;uscita dell&#39;operazione.
