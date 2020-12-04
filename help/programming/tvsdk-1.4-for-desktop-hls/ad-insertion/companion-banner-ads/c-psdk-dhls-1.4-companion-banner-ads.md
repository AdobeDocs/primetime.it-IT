---
description: TVSDK supporta i banner pubblicitari di compagnia, che sono annunci che accompagnano un annuncio lineare e spesso rimangono sulla pagina dopo la fine dell'annuncio lineare. La vostra applicazione è responsabile della visualizzazione dei banner associati forniti con un annuncio lineare.
seo-description: TVSDK supporta i banner pubblicitari di compagnia, che sono annunci che accompagnano un annuncio lineare e spesso rimangono sulla pagina dopo la fine dell'annuncio lineare. La vostra applicazione è responsabile della visualizzazione dei banner associati forniti con un annuncio lineare.
seo-title: Annunci per banner
title: Annunci per banner
uuid: 388a1683-342c-4f3b-97c8-cfcb6c5cfee1
translation-type: tm+mt
source-git-commit: 8ff38bdc1a7ff9732f7f1fae37f64d0e1113ff40
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 0%

---


# Annunci per banner completi {#companion-banner-ads}

TVSDK supporta i banner pubblicitari di compagnia, che sono annunci che accompagnano un annuncio lineare e spesso rimangono sulla pagina dopo la fine dell&#39;annuncio lineare. La vostra applicazione è responsabile della visualizzazione dei banner associati forniti con un annuncio lineare.

Quando visualizzate annunci di accompagnamento, attenetevi alle seguenti raccomandazioni:

* Tentate di presentare tutti gli annunci di banner pubblicitari associati a un video pubblicitari che si adattano al layout del vostro lettore.
* Presentate un banner complementare solo se disponete di una posizione che corrisponda esattamente a altezza e larghezza specificate.

   >[!TIP]
   >
   >Non ridimensionate il banner.

* Presentate i banner di accompagnamento il prima possibile dopo l’inizio dell’annuncio.
* Non sovrapponete il contenitore di annunci/video principale con i banner complementari.
* Continuate a visualizzare i banner complementari dopo la fine dell’annuncio.

   Lo standard prevede la visualizzazione di ciascun banner complementare fino a quando non si dispone di una sostituzione per questo banner.

## Dati del banner della compagnia {#companion-banner-data}

Il contenuto di un AdBannerAsset descrive un banner complementare.

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

L&#39;evento `AdPlaybackEvent.AD_STARTED` restituisce un&#39;istanza `Ad` che contiene una proprietà `companionAssets` ( `Vector.<AdAsset>`).
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
   <td colname="col1"> width </td> 
   <td colname="col2"> Larghezza del banner di accompagnamento, in pixel. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> height </td> 
   <td colname="col2"> Altezza del banner ausiliario, in pixel. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> tipo di risorsa </td> 
   <td colname="col2">Il tipo di risorsa per il banner ausiliario: 
    <ul id="ul_A067787FE49E4B6095BE0AC1D447DBB3"> 
     <li id="li_02B7224C67004095B3F6E50FD21E507E">html: I dati si trovano nel codice HTML. </li> 
     <li id="li_5F37E14472424F808C6094F42009E676">iframe: I dati sono un URL iframe (src). </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> dati banner </td> 
   <td colname="col2"> I dati del tipo specificato da <span class="codeph"> resourceType</span> per il banner ausiliario. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> URL statico </td> 
   <td colname="col2"> <p>A volte, il banner ausiliario ha anche un URL statico che è un URL diretto per l'immagine o per un <span class="filepath"> .swf</span> (banner Flash). </p> <p>Se non desiderate utilizzare html o iframe, potete utilizzare un URL diretto a un’immagine o un file SWF per visualizzare invece il banner nell’area di visualizzazione dell’Flash. In questo caso, potete utilizzare staticURL per visualizzare il banner. </p> <p>Importante:  È necessario verificare se l'URL statico è una stringa valida, perché questa proprietà potrebbe non essere sempre disponibile. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Visualizza annunci banner {#display-banner-ads}

Per visualizzare gli annunci per banner, dovete creare istanze di banner e consentire a TVSDK di ascoltare gli eventi relativi agli annunci.

TVSDK fornisce un elenco di banner pubblicitari associati a un annuncio lineare tramite l&#39;evento `AdPlaybackEvent.AD_STARTED`.

I manifesti possono specificare annunci banner complementari per:

* Snippet HTML
* URL di una pagina iFrame
* URL di un’immagine statica o di un file SWF di Flash di Adobi 

Per ogni annuncio aggiuntivo complementare, TVSDK indica quali tipi sono disponibili per l’applicazione.

Aggiungete un listener per l&#39;evento `AdPlaybackEvent.AD_STARTED` che esegue le seguenti operazioni:

1. Cancella gli annunci esistenti nell&#39;istanza del banner.

1. Ottiene l&#39;elenco degli annunci complementari da `Ad.companionAssets`.

1. Se l&#39;elenco degli annunci complementari non è vuoto, ripetete l&#39;operazione sull&#39;elenco per le istanze del banner.

   Ogni istanza del banner ( un `AdBannerAsset`) contiene informazioni quali larghezza, altezza, tipo di risorsa (html, iframe o statico) e dati necessari per visualizzare il banner ausiliario.

1. Se un annuncio video non contiene annunci pubblicitari associati, l’elenco delle risorse ausiliarie non contiene dati per tale annuncio video.

   Per visualizzare un annuncio di visualizzazione indipendente, aggiungete la logica allo script per eseguire un tag di annuncio di visualizzazione normale DFP (DoubleClick for Publishers) nell&#39;istanza di banner appropriata.

1. Invia le informazioni sul banner a una funzione sulla pagina, in genere JavaScript, utilizzando `ExternalInterface`, che visualizza i banner in una posizione appropriata.

   In genere si tratta di un `div` e la funzione utilizza il `div ID` per visualizzare il banner. Ad esempio:

   Aggiungete il listener di eventi:

   ```js
   _player.addEventListener(AdobePSDK.PSDKEventType.AD_STARTED, onAdStarted);
   ```

   Implementare il gestore di listener:

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
