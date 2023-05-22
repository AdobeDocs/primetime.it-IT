---
description: TVSDK supporta gli annunci banner correlati, ovvero gli annunci che accompagnano un annuncio lineare e che spesso rimangono sulla pagina al termine dell’annuncio lineare. L'applicazione è responsabile della visualizzazione dei banner correlati forniti con un annuncio lineare.
title: Banner pubblicitari
exl-id: c10a38ec-acbb-4e84-aff2-c93c9b1cec81
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 0%

---

# Banner pubblicitari {#companion-banner-ads}

TVSDK supporta gli annunci banner correlati, ovvero gli annunci che accompagnano un annuncio lineare e che spesso rimangono sulla pagina al termine dell’annuncio lineare. L&#39;applicazione è responsabile della visualizzazione dei banner correlati forniti con un annuncio lineare.

Quando visualizzi gli annunci correlati, segui queste raccomandazioni:

* Tenta di presentare tutti gli annunci banner associati a un annuncio video che rientrano nel layout del lettore.
* Presentare un banner correlato solo se la posizione corrisponde esattamente all&#39;altezza e alla larghezza specificate.

   >[!TIP]
   >
   >Non ridimensionare il banner.

* Presenta il banner/i correlato/i il prima possibile dopo l’inizio dell’annuncio.
* Non sovrapporre il contenitore principale annuncio/video con i banner correlati.
* Continua a visualizzare i banner associati dopo la fine dell’annuncio.

   Lo standard prevede la visualizzazione di ogni banner complementare fino a quando non si dispone di un banner sostitutivo.

## Dati banner aziendale {#companion-banner-data}

Il contenuto di una risorsa AdBanner descrive un banner correlato.

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

Il `AdPlaybackEvent.AD_STARTED` l&#39;evento restituisce un `Ad` istanza che contiene un `companionAssets` proprietà ( `Vector.<AdAsset>`).
Ogni `AdAsset` fornisce informazioni sulla visualizzazione della risorsa.

<table id="table_760C885E2DCA4BE983CC57FDA7BD5B14"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Informazioni disponibili </th> 
   <th colname="col2" class="entry"> Descrizione </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> larghezza </td> 
   <td colname="col2"> Larghezza in pixel del banner correlato. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> altezza </td> 
   <td colname="col2"> Altezza del banner correlato in pixel. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> tipo di risorsa </td> 
   <td colname="col2">Il tipo di risorsa per questo banner correlato: 
    <ul id="ul_A067787FE49E4B6095BE0AC1D447DBB3"> 
     <li id="li_02B7224C67004095B3F6E50FD21E507E">html: i dati sono nel codice HTML. </li> 
     <li id="li_5F37E14472424F808C6094F42009E676">iframe: i dati sono un URL iframe (src). </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> dati banner </td> 
   <td colname="col2"> Dati del tipo specificato da <span class="codeph"> resourceType</span> per questo banner. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> URL statico </td> 
   <td colname="col2"> <p>A volte, il banner correlato ha anche un URL statico che è un URL diretto all’immagine o a un <span class="filepath"> .swf</span> (banner flash). </p> <p>Se non desideri utilizzare html o iframe, puoi utilizzare un URL diretto per un’immagine o un file swf per visualizzare il banner nella fase di Flash. In questo caso, puoi utilizzare staticURL per visualizzare il banner. </p> <p>Importante: è necessario verificare se l’URL statico è una stringa valida, perché questa proprietà potrebbe non essere sempre disponibile. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Visualizza banner pubblicitari {#display-banner-ads}

Per visualizzare gli annunci banner, devi creare istanze di banner e consentire a TVSDK di ascoltare eventi relativi agli annunci.

TVSDK fornisce un elenco di banner pubblicitari correlati associati a un annuncio lineare tramite `AdPlaybackEvent.AD_STARTED` evento.

I manifesti possono specificare gli annunci banner correlati in base a:

* Un frammento di HTML
* URL di una pagina iFrame
* URL di un&#39;immagine statica o di un file SWF di Flash di Adobe

Per ogni annuncio correlato, TVSDK indica i tipi disponibili per l’applicazione.

Aggiungere un listener per `AdPlaybackEvent.AD_STARTED` evento che esegue le seguenti operazioni:

1. Cancella gli annunci esistenti nell’istanza del banner.

1. Ottiene l’elenco degli annunci correlati da `Ad.companionAssets`.

1. Se l’elenco degli annunci correlati non è vuoto, scorri l’elenco per le istanze del banner.

   Ogni istanza del banner ( an `AdBannerAsset`) contiene informazioni quali larghezza, altezza, tipo di risorsa (html, iframe o statica) e dati necessari per visualizzare il banner correlato.

1. Se un annuncio video non ha annunci correlati prenotati con esso, l’elenco delle risorse correlate non contiene dati per tale annuncio video.

   Per visualizzare un annuncio di visualizzazione autonomo, aggiungi la logica allo script per eseguire un normale tag annuncio di visualizzazione DFP (DoubleClick for Publishers) nell’istanza del banner appropriata.

1. Invia le informazioni sul banner a una funzione sulla pagina, in genere JavaScript, utilizzando `ExternalInterface`, che visualizza i banner in una posizione appropriata.

   Questo è di solito un `div`, e la tua funzione utilizza `div ID` per visualizzare il banner. Ad esempio:

   Aggiungi il listener di eventi:

   ```js
   _player.addEventListener(AdobePSDK.PSDKEventType.AD_STARTED, onAdStarted);
   ```

   Implementa il gestore listener:

   ```js
   private function onAdStarted(event:AdPlaybackEvent):void { 
       // check if there are any companion banner 
       if (event.ad && event.ad.companionAssets  
                    && event.ad.companionAssets.length > 0) { 
           for each (var banner:AdBannerAsset in event.ad.companionAssets) { 
               if (ExternalInterface.available) { 
                   //-- call the java script that will handle the banner display. 
                   ExternalInterface.call('addBanner', banner.resourceType,  
                       banner.width, banner.height, banner.bannerData); 
               } 
           } 
       }  
       //...        
   }
   ```

   Esempio di JavaScript per gestire la visualizzazione:

   ```js
   function addBanner(resourceType, width, height, data) { 
       console.log(resourceType + "," +  width + "," +  height); 
   
   //Assume an html element on the page with id like 'banner300x250' 
       var bannerDiv = document.getElementById('banner' + width +  
           'x' + height);  
       if (bannerDiv != null) { 
           if (resourceType == "html") { // for html resource 
               bannerDiv.innerHTML = data; 
           } 
           else if (resourceType == "iframe") { // for iframe resource 
               bannerDiv.innerHTML = "<iframe src='" + data +  
                   "' width='100%' height='100%'></iframe>"; 
           } 
       } 
   }
   ```
