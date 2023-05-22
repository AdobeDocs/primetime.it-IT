---
description: Per ogni nuovo contenuto video, inizializza un’istanza MediaResource con informazioni sul contenuto video e carica la risorsa multimediale. La classe MediaResource rappresenta il contenuto da caricare dall'istanza MediaPlayer.
title: Creare una risorsa multimediale
exl-id: cda70f91-7f30-4e37-9dfa-888b707e3d61
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# Creare una risorsa multimediale {#create-a-media-resource}

Per ogni nuovo contenuto video, inizializza un’istanza MediaResource con informazioni sul contenuto video e carica la risorsa multimediale. La classe MediaResource rappresenta il contenuto da caricare dall&#39;istanza MediaPlayer.

1. Creare un `MediaResource` trasmettendo informazioni sui mezzi di comunicazione alla `MediaResource` costruttore.

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
    <td colname="col2"> <p>Stringa che rappresenta l’URL del manifesto o della playlist del contenuto multimediale. </p> </td> 
    </tr> 
    <tr> 
    <td colname="col1"> <p>tipo </p> </td> 
    <td colname="col2"> <p>Uno dei seguenti membri della <span class="codeph"> MediaResource.Type </span> enumerazione che corrisponde al tipo di file indicato: 
    <ul id="ul_72636C41CA7E4538A3BE11A79E0282FC"> 
    <li id="li_070960200DEB40E992C58FCB8909AEA3"> <span class="codeph"> HLS </span> - M3U8 </li> 
    </ul> </p> </td> 
    </tr> 
    <tr> 
    <td colname="col1"> <p>metadati </p> </td> 
    <td colname="col2"> <p>Un'istanza di <span class="codeph"> Metadati </span> , che potrebbe contenere informazioni personalizzate sul contenuto da caricare. </p> <p>Esempi di contenuto sono il contenuto alternativo o l’annuncio da inserire all’interno del contenuto principale. Se utilizzi la pubblicità, imposta <span class="codeph"> AuditudeSettings </span>. Per ulteriori informazioni, consulta <a href="../../../tvsdk-1.4-for-android/ad-insertion/ad-insertion-metadata/android-1.4-ad-insertion-metadata-set-up.md" format="dita" scope="local"> Metadati Ad Insertion </a>. </p> </td> 
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
   >A questo punto, puoi utilizzare `MediaResource` funzioni di accesso (getter) per esaminare il tipo, l’URL e i metadati della risorsa.

1. Carica la risorsa multimediale utilizzando quanto segue:

   * Istanza MediaPlayer in uso.

      Per ulteriori informazioni, consulta [Caricare una risorsa multimediale in MediaPlayer](../../../tvsdk-1.4-for-android/ui-configure/mediaplayer-initialize-for-video/android-1.4-media-resource-load.md).
   * A `MediaPlayerItemLoader` Per ulteriori informazioni, consulta [Caricare una risorsa multimediale tramite MediaPlayerItemLoader](../../../tvsdk-1.4-for-android/ui-configure/mediaplayer-initialize-for-video/android-1.4-media-mediaplayeritemloader.md).
   >[!IMPORTANT]
   >
   >Non caricare la risorsa multimediale su un thread in background. La maggior parte delle operazioni TVSDK devono essere eseguite sul thread principale e la loro esecuzione su un thread in background può causare la generazione di un errore e l&#39;uscita dall&#39;operazione.
