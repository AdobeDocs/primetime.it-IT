---
description: Per visualizzare gli annunci pubblicitari dei banner, devi creare istanze di banner e consentire a TVSDK del browser di rilevare gli eventi relativi agli annunci.
title: Visualizza banner pubblicitari
exl-id: 331c10a4-ae31-4d3b-aaca-9497e2970ecf
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---

# Visualizza banner pubblicitari {#display-banner-ads}

Per visualizzare gli annunci pubblicitari dei banner, devi creare istanze di banner e consentire a TVSDK del browser di rilevare gli eventi relativi agli annunci.

Browser TVSDK fornisce un elenco di banner pubblicitari correlati associati a un annuncio lineare tramite `AdobePSDK.PSDKEventType.AD_STARTED` evento.

I manifesti possono specificare gli annunci banner correlati in base a:

* Un frammento di HTML
* URL di una pagina iFrame
* URL di un&#39;immagine statica o di un file SWF di Flash di Adobe

Per ogni annuncio correlato, il TVSDK del browser indica i tipi disponibili per l’applicazione.

Aggiungere un listener per l&#39;evento `AdobePSDK.PSDKEventType.AD_STARTED` che effettua le seguenti operazioni:
1. Cancella gli annunci esistenti nell’istanza del banner.
1. Ottiene l’elenco degli annunci correlati da `Ad.getCompanionAssets`.
1. Se l’elenco degli annunci correlati non è vuoto, scorri l’elenco per le istanze del banner.

   Ogni istanza del banner (un `AdBannerAsset`) contiene informazioni quali larghezza, altezza, tipo di risorsa (html, iframe o statica) e dati necessari per visualizzare il banner correlato.
1. Se un annuncio video non ha annunci correlati prenotati con esso, l’elenco delle risorse correlate non contiene dati per tale annuncio video.
1. Invia le informazioni sul banner a una funzione sulla pagina che visualizza i banner in una posizione appropriata.

   Questo è di solito un `div`, e la tua funzione utilizza `div ID` per visualizzare il banner. Ad esempio:

   Aggiungi il listener di eventi:

   ```js
   _player.addEventListener(AdobePSDK.PSDKEventType.AD_STARTED, onAdStarted);
   ```

   Implementa il gestore listener:

   ```js
   private function onAdStarted(event:AdPlaybackEvent):void 
   { 
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
   function displayCompanion (resourceType, width, height, data) { 
       console.log(resourceType + "," +  width + "," +  height); 
       var bannerDiv = document.getElementById('banner' + width + 'x' + height);  
   
       // Assuming that there is an HTML element on the page  
       // with an id of "banner300x250", for example 
       if (bannerDiv !== null) { 
           bannerDiv.innerHTML = data; 
       } 
   }
   ```
