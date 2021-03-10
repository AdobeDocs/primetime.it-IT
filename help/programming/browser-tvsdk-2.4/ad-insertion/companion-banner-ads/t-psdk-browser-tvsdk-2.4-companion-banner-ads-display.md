---
description: Per visualizzare gli annunci banner, devi creare istanze di banner e consentire al browser TVSDK di ascoltare gli eventi relativi agli annunci.
title: Visualizza annunci banner
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---


# Visualizza annunci banner {#display-banner-ads}

Per visualizzare gli annunci banner, devi creare istanze di banner e consentire al browser TVSDK di ascoltare gli eventi relativi agli annunci.

Il browser TVSDK fornisce un elenco di banner pubblicitari associati a un annuncio lineare tramite l&#39;evento `AdobePSDK.PSDKEventType.AD_STARTED` .

I manifesti possono specificare annunci di banner complementari per:

* Frammento HTML
* URL di una pagina iFrame
* URL di un’immagine statica o di un file SWF di Flash di Adobe

Per ogni annuncio correlato, Browser TVSDK indica quali tipi sono disponibili per l&#39;applicazione.

Aggiungi un listener per l&#39;evento `AdobePSDK.PSDKEventType.AD_STARTED` che esegue le seguenti operazioni:
1. Cancella gli annunci esistenti nell&#39;istanza del banner.
1. Ottiene l&#39;elenco degli annunci companion da `Ad.getCompanionAssets`.
1. Se l’elenco degli annunci associati non è vuoto, ripeti l’errore sopra l’elenco per le istanze del banner.

   Ogni istanza del banner (un elemento `AdBannerAsset`) contiene informazioni quali larghezza, altezza, tipo di risorsa (html, iframe o statico) e dati necessari per visualizzare il banner correlato.
1. Se un annuncio video non ha annunci correlati prenotati con esso, l’elenco delle risorse correlate non contiene dati per quell’annuncio video.
1. Invia le informazioni sul banner a una funzione nella pagina in cui vengono visualizzati i banner in una posizione appropriata.

   In genere si tratta di una `div` e la funzione utilizza `div ID` per visualizzare il banner. Ad esempio:

   Aggiungi il listener di eventi:

   ```js
   _player.addEventListener(AdobePSDK.PSDKEventType.AD_STARTED, onAdStarted);
   ```

   Implementa il gestore di listener:

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

