---
description: MediaPlayer fornisce una funzione notificationClick() che invia eventi correlati agli annunci durante la riproduzione di un annuncio selezionabile. Questi eventi forniscono informazioni su annunci e interruzioni pubblicitarie che l'app può utilizzare per fornire funzionalità di click-through.
seo-description: MediaPlayer fornisce una funzione notificationClick() che invia eventi correlati agli annunci durante la riproduzione di un annuncio selezionabile. Questi eventi forniscono informazioni su annunci e interruzioni pubblicitarie che l'app può utilizzare per fornire funzionalità di click-through.
seo-title: Gestire gli annunci cliccabili
title: Gestire gli annunci cliccabili
uuid: 5d3c9d36-60d7-4272-a523-7d1fe0e1615f
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Gestire gli annunci cliccabili {#handle-clickable-ads}

MediaPlayer fornisce una funzione notificationClick() che invia eventi correlati agli annunci durante la riproduzione di un annuncio selezionabile. Questi eventi forniscono informazioni su annunci e interruzioni pubblicitarie che l&#39;app può utilizzare per fornire funzionalità di click-through.

MediaPlayer attiva i seguenti eventi quando viene riprodotto un annuncio selezionabile:

* `AdobePSDK.PSDKEventType.AD_STARTED`
* `AdobePSDK.PSDKEventType.AD_CLICKED`
* `AdobePSDK.PSDKEventType.AD_COMPLETED`

L&#39; `AdClickedEvent` elenco contiene le informazioni necessarie per elaborare la funzione click-through.

1. Consente agli utenti di fare clic sugli annunci cliccabili per controllare il lettore.

   Può trattarsi di un pulsante o di qualsiasi altro elemento per acquisire il clic dell&#39;utente.
1. Aggiungete un listener di eventi per l&#39;evento ad click dell&#39;utente.

   Ad esempio:

   ```
   document.getElementById([ 
   <i>your_click_control_id</i>]).addEventListener("click", onAdClick);
   ```

1. Aggiungete un gestore per l&#39;evento click dell&#39;utente.

   Questo gestore deve richiedere a MediaPlayer di attivare l&#39; `AdClicked` evento.

   ```
   onAdClick = function (event) { 
       // Get a reference to your player 
       var player = getPlayer(); 
       if (player) { 
           // Call the MediaPlayer's notifyClick function 
           // which gets MediaPlayer to fire AdClicked 
           player.notifyClick(); 
       } 
   } 
   ```

1. Aggiungete i listener di eventi per le notifiche di inizio e inizio di MediaPlayer e fate clic su di esso, quindi aggiungete le notifiche di completamento.

   ```
    <i>your_player</i>().addEventListener(AdobePSDK.PSDKEventType.AD_STARTED, onAdStarted); 
   
    <i>your_player</i>().addEventListener(AdobePSDK.PSDKEventType.AD_COMPLETED, onAdCompleted);
   
    <i>your_player</i>().addEventListener(AdobePSDK.PSDKEventType.AD_CLICKED, onAdClickedEvent);
   ```

1. Aggiungete i gestori di eventi.
a. Gestite l’evento di inizio annuncio.
Ciò potrebbe fare qualsiasi cosa, ad esempio configurare l&#39;interfaccia utente per l&#39;utente.

   ```
   onAdStarted = function (event) { 
       if (clickAddButton && event && event.ad) { 
           var adClick = event.ad.primaryAsset && event.ad.primaryAsset.adClick; 
           if (adClick && adClick.isValid) { 
               // Do some initial processing  
               // when the ad starts, prior 
               // to the user's click. 
           } 
       } 
   }
   ```

   b. Gestite l’evento con clic dell’annuncio.
In questo esempio, otteniamo informazioni sugli annunci dall&#39;evento e apriamo una nuova finestra del browser utilizzando tali informazioni:

   ```
   onAdClickedEvent = function (event) { 
       if (event && event.ad) { 
           var adClick = event.adClick; 
           if (!(adClick && adClick.isValid)) { 
               adClick = event.ad.primaryAsset && event.ad.primaryAsset.adClick; 
           } 
           if (adClick && adClick.isValid) 
           { 
               // Do something with the currently playing ad 
               window.open(adClick.url); 
           } 
       } 
   }
   ```

   c. Gestite l’evento annuncio completato.

   ```
   onAdCompleted = function (event) { 
       if (clickAddButton) { 
           clickAddButton.setAttribute('hidden', 'true'); 
       } 
   }
   ```
