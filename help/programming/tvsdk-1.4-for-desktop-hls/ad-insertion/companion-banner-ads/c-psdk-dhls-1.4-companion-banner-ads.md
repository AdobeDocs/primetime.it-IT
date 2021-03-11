---
description: TVSDK supporta annunci per banner complementari, che sono annunci che accompagnano un annuncio lineare e spesso rimangono sulla pagina dopo la fine dell’annuncio lineare. La tua applicazione è responsabile della visualizzazione dei banner complementari che sono forniti con un annuncio lineare.
title: Annunci banner
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 0%

---


# Annunci per banner pubblicitari {#companion-banner-ads}

TVSDK supporta annunci per banner complementari, che sono annunci che accompagnano un annuncio lineare e spesso rimangono sulla pagina dopo la fine dell’annuncio lineare. La tua applicazione è responsabile della visualizzazione dei banner complementari che sono forniti con un annuncio lineare.

Quando si visualizzano gli annunci companion, attenersi alle seguenti raccomandazioni:

* Tenta di presentare il numero di annunci banner di un annuncio video come si adatterà al layout del tuo giocatore.
* Presentare un banner complementare solo se si dispone di una posizione che corrisponde esattamente alla sua altezza e larghezza specificate.

   >[!TIP]
   >
   >Non ridimensionare il banner.

* Presenta i banner associati il prima possibile dopo l’inizio dell’annuncio.
* Non sovrapporre il contenitore principale annuncio/video con banner complementari.
* Continua a visualizzare i banner complementari dopo la fine dell’annuncio.

   Lo standard è quello di visualizzare ogni banner associato fino a quando non si dispone di una sostituzione per questo banner.

## Dati banner Companion {#companion-banner-data}

Il contenuto di un AdBannerAsset descrive un banner correlato.

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

L&#39;evento `AdPlaybackEvent.AD_STARTED` restituisce un&#39;istanza `Ad` che contiene una proprietà `companionAssets` ( `Vector.<AdAsset>`).
Ogni elemento `AdAsset` fornisce informazioni sulla visualizzazione della risorsa.

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
   <td colname="col2"> Larghezza del banner correlato in pixel. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> altezza </td> 
   <td colname="col2"> Altezza del banner correlato in pixel. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> tipo di risorsa </td> 
   <td colname="col2">Tipo di risorsa per il banner correlato: 
    <ul id="ul_A067787FE49E4B6095BE0AC1D447DBB3"> 
     <li id="li_02B7224C67004095B3F6E50FD21E507E">html I dati sono nel codice HTML. </li> 
     <li id="li_5F37E14472424F808C6094F42009E676">iframe: I dati sono un URL iframe (src). </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> dati banner </td> 
   <td colname="col2"> I dati del tipo specificato da <span class="codeph"> resourceType</span> per questo banner correlato. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> URL statico </td> 
   <td colname="col2"> <p>A volte, il banner associato ha anche un URL statico che è un URL diretto all'immagine o a un <span class="filepath"> .swf</span> (banner flash). </p> <p>Se non desideri utilizzare html o iframe, puoi utilizzare un URL diretto per un’immagine o un swf per visualizzare il banner nella fase di Flash. In questo caso, puoi utilizzare staticURL per visualizzare il banner. </p> <p>Importante:  È necessario verificare se l’URL statico è una stringa valida, perché questa proprietà potrebbe non essere sempre disponibile. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Visualizza annunci banner {#display-banner-ads}

Per visualizzare gli annunci banner, devi creare istanze banner e consentire a TVSDK di ascoltare gli eventi relativi agli annunci.

TVSDK fornisce un elenco di banner pubblicitari associati a un annuncio lineare tramite l&#39;evento `AdPlaybackEvent.AD_STARTED` .

I manifesti possono specificare annunci di banner complementari per:

* Frammento HTML
* URL di una pagina iFrame
* URL di un’immagine statica o di un file SWF di Flash di Adobe

Per ogni annuncio correlato, TVSDK indica quali tipi sono disponibili per l’applicazione.

Aggiungi un listener per l&#39;evento `AdPlaybackEvent.AD_STARTED` che esegue le seguenti operazioni:

1. Cancella gli annunci esistenti nell&#39;istanza del banner.

1. Ottiene l&#39;elenco degli annunci companion da `Ad.companionAssets`.

1. Se l’elenco degli annunci associati non è vuoto, ripeti l’errore sopra l’elenco per le istanze del banner.

   Ogni istanza di banner ( an `AdBannerAsset`) contiene informazioni quali larghezza, altezza, tipo di risorsa (html, iframe o statico) e dati necessari per visualizzare il banner correlato.

1. Se un annuncio video non ha annunci correlati prenotati con esso, l’elenco delle risorse correlate non contiene dati per quell’annuncio video.

   Per mostrare un annuncio di visualizzazione indipendente, aggiungi la logica al tuo script per eseguire un tag di annunci di visualizzazione normale DFP (DoubleClick for Publishers) nell’istanza di banner appropriata.

1. Invia le informazioni sul banner a una funzione nella pagina, in genere JavaScript, utilizzando `ExternalInterface`, che visualizza i banner in una posizione appropriata.

   In genere si tratta di una `div` e la funzione utilizza `div ID` per visualizzare il banner. Ad esempio:

   Aggiungi il listener di eventi:

   ```js
   _player.addEventListener(AdobePSDK.PSDKEventType.AD_STARTED, onAdStarted);
   ```

   Implementa il gestore di listener:

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
