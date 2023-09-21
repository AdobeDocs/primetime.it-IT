---
description: La classe MediaResource rappresenta il contenuto da caricare dall'istanza MediaPlayer.
title: Creare una risorsa multimediale
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---

# Creare una risorsa multimediale {#create-a-media-resource}

La classe MediaResource rappresenta il contenuto da caricare dall&#39;istanza MediaPlayer.

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
    <td colname="col2"> <p>Uno dei seguenti membri della <span class="codeph"> MediaResource.Type </span> enumerazione che corrisponde al tipo di file indicato: </p> <p> 
    <ul id="ul_E9689FA06DC94BF4848F16E1F2F01A59"> 
    <li id="li_83A14B96CDC648C6AF6F5FA745343E1F"> <span class="codeph"> MP4 </span> - Formato di file multimediale di base ISO (MP4) </li> 
    <li id="li_FCD355151515412D9A78C3815DD09129"> <span class="codeph"> HLS </span> - M3U8 </li> 
    <li id="li_9D3D306D49264830AC6EFB1F49524A3B"> <span class="codeph"> TRATTINO </span> - MPD </li> 
    </ul> </p> <p></p> </td> 
    </tr> 
    <tr> 
    <td colname="col1"> <p>metadati </p> </td> 
    <td colname="col2"> <p>Un'istanza di <span class="codeph"> Metadati </span> , che potrebbe contenere informazioni personalizzate sul contenuto da caricare. Esempi di contenuto sono il contenuto alternativo o l’annuncio da inserire all’interno del contenuto principale. Se utilizzi la pubblicità, imposta <span class="codeph"> AuditudeSettings </span> prima di utilizzare questo costruttore. Per ulteriori informazioni, consulta <a href="../../ad-insertion/ad-insertion-metadata/c-psdk-browser-tvsdk-2.4-ad-insertion-metadata.md">Ad-insertion-metadata</a>. </p> <p>Suggerimento: se necessario, puoi forzare il fallback del Flash utilizzando <span class="codeph"> forceFlash </span> durante la creazione di una risorsa multimediale. Questo può essere utile perché al momento non tutte le funzioni (come i flussi di lavoro Live Ad) sono supportati nel TVSDK del browser. Il fallback del Flash viene utilizzato per riprodurre i contenuti video. </p> </td> 
    </tr> 
    </tbody> 
   </table>

   >[!IMPORTANT]
   >
   >Browser TVSDK supporta la riproduzione solo per tipi specifici di contenuto. Se tenti di caricare un altro tipo di contenuto, il TVSDK del browser invia un evento di errore.

   Il codice seguente crea un `MediaResource` istanza:

   ```js
   //create a MediaResource instance pointing to some HLS content 
   Metadata metadata = //TODO: create metadata here 
   mediaResource = new AdobePSDK.MediaResource ( 
         "https://www.example.com/video/some-video.m3u8", 
         AdobePSDK.MediaResourceType.HLS,  
         metadata);
   ```

   >[!TIP]
   >
   >In qualsiasi momento successivo, puoi utilizzare `MediaResource` funzioni di accesso (getter) per esaminare il tipo, l’URL e i metadati della risorsa.

1. Carica l’istanza MediaPlayer. Per ulteriori informazioni, consulta [Caricare una risorsa multimediale in MediaPlayer](../../content-playback-options-browser-tvsdk/mediaplayer-initialize-for-video/t-psdk-browser-tvsdk-2.4-media-resource-load.md).
