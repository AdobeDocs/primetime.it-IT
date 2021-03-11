---
description: MediaPlayer fornisce una funzione notifyClick() che invia eventi correlati agli annunci quando un annuncio è in riproduzione. Questi eventi forniscono informazioni sugli annunci e sulle interruzioni pubblicitarie che l’app può utilizzare per fornire funzionalità di click-through.
title: Gestire gli annunci cliccabili
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---


# Gestire gli annunci cliccabili {#handle-clickable-ads}

MediaPlayer fornisce una funzione notifyClick() che invia eventi correlati agli annunci quando un annuncio è in riproduzione. Questi eventi forniscono informazioni sugli annunci e sulle interruzioni pubblicitarie che l’app può utilizzare per fornire funzionalità di click-through.

MediaPlayer genera i seguenti eventi quando viene eseguito un annuncio selezionabile:

* `AdobePSDK.PSDKEventType.AD_STARTED`
* `AdobePSDK.PSDKEventType.AD_CLICKED`
* `AdobePSDK.PSDKEventType.AD_COMPLETED`

Il `AdClickedEvent` contiene le informazioni necessarie per elaborare la funzione di click-through.

1. Fornisci un controllo nel tuo lettore affinché gli utenti clicchino sugli annunci cliccabili.

   Può trattarsi di un pulsante o di qualsiasi altro elemento per acquisire il clic dell’utente.
1. Aggiungi un listener di eventi per l&#39;evento ad click dell&#39;utente.

   Ad esempio:

   ```
   document.getElementById([ 
   <i>your_click_control_id</i>]).addEventListener("click", onAdClick);
   ```

1. Aggiungi un gestore per l&#39;evento click dell&#39;utente.

   Questo gestore deve richiedere a MediaPlayer di attivare l&#39;evento `AdClicked`.

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

1. Aggiungi i listener di eventi per le notifiche di inizio e inizio dell&#39;annuncio MediaPlayer, l&#39;annuncio ha fatto clic e l&#39;annuncio è stato completato.

   ```
    <i>your_player</i>().addEventListener(AdobePSDK.PSDKEventType.AD_STARTED, onAdStarted); 
   
    <i>your_player</i>().addEventListener(AdobePSDK.PSDKEventType.AD_COMPLETED, onAdCompleted);
   
    <i>your_player</i>().addEventListener(AdobePSDK.PSDKEventType.AD_CLICKED, onAdClickedEvent);
   ```

1. Aggiungi gestori eventi.
a) Gestisci l&#39;evento di inizio annuncio.
Questo può fare qualsiasi cosa, ad esempio la configurazione dell’interfaccia utente per l’utente.

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

   b) Gestisci l&#39;evento con clic dell&#39;annuncio.
In questo esempio, otteniamo informazioni sugli annunci dall’evento e apriamo una nuova finestra del browser utilizzando tali informazioni:

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

   c. Gestisci l’evento annuncio completato.

   ```
   onAdCompleted = function (event) { 
       if (clickAddButton) { 
           clickAddButton.setAttribute('hidden', 'true'); 
       } 
   }
   ```
