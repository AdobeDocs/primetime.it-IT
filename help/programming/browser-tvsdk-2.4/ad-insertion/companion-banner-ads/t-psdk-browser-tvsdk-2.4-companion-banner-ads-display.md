---
description: Per visualizzare gli annunci per banner, dovete creare istanze di banner e consentire a Browser TVSDK di ascoltare gli eventi relativi agli annunci.
seo-description: Per visualizzare gli annunci per banner, dovete creare istanze di banner e consentire a Browser TVSDK di ascoltare gli eventi relativi agli annunci.
seo-title: Visualizza annunci banner
title: Visualizza annunci banner
uuid: aabc126e-b3aa-42dd-ab50-a7db8e324c50
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---


# Visualizza annunci banner {#display-banner-ads}

Per visualizzare gli annunci per banner, dovete creare istanze di banner e consentire a Browser TVSDK di ascoltare gli eventi relativi agli annunci.

Browser TVSDK fornisce un elenco di banner pubblicitari associati a un annuncio lineare tramite l&#39;evento `AdobePSDK.PSDKEventType.AD_STARTED`.

I manifesti possono specificare annunci banner complementari per:

* Snippet HTML
* URL di una pagina iFrame
* URL di un’immagine statica o di un file SWF di Flash di Adobi 

Per ogni annuncio aggiuntivo, Browser TVSDK indica quali tipi sono disponibili per l&#39;applicazione.

Aggiungete un listener per l&#39;evento `AdobePSDK.PSDKEventType.AD_STARTED` che esegue le seguenti operazioni:
1. Cancella gli annunci esistenti nell&#39;istanza del banner.
1. Ottiene l&#39;elenco degli annunci complementari da `Ad.getCompanionAssets`.
1. Se l&#39;elenco degli annunci complementari non è vuoto, ripetete l&#39;operazione sull&#39;elenco per le istanze del banner.

   Ogni istanza del banner (un `AdBannerAsset`) contiene informazioni quali larghezza, altezza, tipo di risorsa (html, iframe o statico) e dati necessari per visualizzare il banner ausiliario.
1. Se un annuncio video non contiene annunci pubblicitari associati, l’elenco delle risorse ausiliarie non contiene dati per tale annuncio video.
1. Invia le informazioni sul banner a una funzione sulla pagina che visualizza i banner in una posizione appropriata.

   In genere si tratta di un `div` e la funzione utilizza il `div ID` per visualizzare il banner. Ad esempio:

   Aggiungete il listener di eventi:

   ```js
   _player.addEventListener(AdobePSDK.PSDKEventType.AD_STARTED, onAdStarted);
   ```

   Implementare il gestore di listener:

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

