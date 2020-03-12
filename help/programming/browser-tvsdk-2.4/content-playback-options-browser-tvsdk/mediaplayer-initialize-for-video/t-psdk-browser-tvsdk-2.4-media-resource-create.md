---
description: La classe MediaResource rappresenta il contenuto da caricare dall'istanza MediaPlayer.
seo-description: La classe MediaResource rappresenta il contenuto da caricare dall'istanza MediaPlayer.
seo-title: Creazione di una risorsa multimediale
title: Creazione di una risorsa multimediale
uuid: c25c037e-e9a0-430c-a150-b75a9ac051b1
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Creazione di una risorsa multimediale {#create-a-media-resource}

La classe MediaResource rappresenta il contenuto da caricare dall&#39;istanza MediaPlayer.

1. Create un `MediaResource` passando le informazioni sul supporto al `MediaResource` costruttore.

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
    <td colname="col2"> <p>Uno dei seguenti membri dell'enumerazione <span class="codeph"> MediaResource.Type </span> che corrisponde al tipo di file indicato: </p> <p> 
    <ul id="ul_E9689FA06DC94BF4848F16E1F2F01A59"> 
    <li id="li_83A14B96CDC648C6AF6F5FA745343E1F"> <span class="codeph"> MP4 </span> - Formato file multimediale base ISO (MP4) </li> 
    <li id="li_FCD355151515412D9A78C3815DD09129"> <span class="codeph"> HLS </span> - M3U8 </li> 
    <li id="li_9D3D306D49264830AC6EFB1F49524A3B"> <span class="codeph"> DASH </span> - MPD </li> 
    </ul> </p> <p></p> </td> 
    </tr> 
    <tr> 
    <td colname="col1"> <p>metadata </p> </td> 
    <td colname="col2"> <p>Un'istanza della <span class="codeph"> classe Metadata </span> , che potrebbe contenere informazioni personalizzate sul contenuto da caricare. Esempi di contenuto sono contenuti alternativi o di annunci da inserire all'interno del contenuto principale. Se si utilizza la pubblicità, impostare <span class="codeph"> AuditudeSettings </span> prima di utilizzare questo costruttore. Per ulteriori informazioni, consultate <a href="../../ad-insertion/ad-insertion-metadata/c-psdk-browser-tvsdk-2.4-ad-insertion-metadata.md">Ad-Insert-metadata</a>. </p> <p>Suggerimento:  Se necessario, potete imporre la fallback Flash usando il parametro <span class="codeph"> forceFlash </span> durante la creazione di una risorsa multimediale. Questa funzione può essere utile perché al momento non tutte le funzioni (come i flussi di lavoro di annunci dal vivo) sono supportate nel browser TVSDK. Il fallback Flash viene utilizzato per riprodurre il contenuto video. </p> </td> 
    </tr> 
    </tbody> 
   </table>

   >[!IMPORTANT]
   >
   >Browser TVSDK supporta la riproduzione solo per tipi specifici di contenuto. Se tentate di caricare qualsiasi altro tipo di contenuto, l&#39;SDK del browser invia un evento di errore.

   Il codice seguente crea un&#39; `MediaResource` istanza:

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
   >In qualsiasi momento successivo, potete utilizzare `MediaResource` accessor (getters) per esaminare il tipo, l&#39;URL e i metadati della risorsa.

1. Caricate l’istanza di MediaPlayer. Per ulteriori informazioni, consultate [Caricare una risorsa multimediale in MediaPlayer](../../content-playback-options-browser-tvsdk/mediaplayer-initialize-for-video/t-psdk-browser-tvsdk-2.4-media-resource-load.md).
