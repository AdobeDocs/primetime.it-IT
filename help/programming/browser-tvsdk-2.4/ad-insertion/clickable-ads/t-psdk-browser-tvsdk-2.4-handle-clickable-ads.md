---
description: MediaPlayer fornisce una funzione notificationClick() che invia eventi relativi agli annunci durante la riproduzione di un annuncio cliccabile. Questi eventi forniscono informazioni su annunci e interruzioni pubblicitarie che l’app può utilizzare per fornire funzionalità di click-through.
title: Gestire gli annunci cliccabili
exl-id: 25738592-f3fe-4f13-b2bb-26a5f942cd18
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---

# Gestire gli annunci cliccabili {#handle-clickable-ads}

MediaPlayer fornisce una funzione notificationClick() che invia eventi relativi agli annunci durante la riproduzione di un annuncio cliccabile. Questi eventi forniscono informazioni su annunci e interruzioni pubblicitarie che l’app può utilizzare per fornire funzionalità di click-through.

Quando viene riprodotto un annuncio cliccabile, MediaPlayer genera i seguenti eventi:

* `AdobePSDK.PSDKEventType.AD_STARTED`
* `AdobePSDK.PSDKEventType.AD_CLICKED`
* `AdobePSDK.PSDKEventType.AD_COMPLETED`

Il `AdClickedEvent` contiene le informazioni necessarie per elaborare la funzione di click-through.

1. Fornisci un controllo nel lettore che consenta agli utenti di fare clic sugli annunci cliccabili.

   Potrebbe trattarsi di un pulsante o di qualsiasi altro elemento per acquisire il clic dell’utente.
1. Aggiungi un listener di eventi per l’evento ad click dell’utente.

   Ad esempio:

   ```
   document.getElementById([ 
   <i>your_click_control_id</i>]).addEventListener("click", onAdClick);
   ```

1. Aggiungi un gestore per l’evento clic dell’utente.

   Questo gestore deve richiedere a MediaPlayer di attivare `AdClicked` evento.

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

1. Aggiungi i listener di eventi per le notifiche di avvio, clic e completamento degli annunci di MediaPlayer.

   ```
    <i>your_player</i>().addEventListener(AdobePSDK.PSDKEventType.AD_STARTED, onAdStarted); 
   
    <i>your_player</i>().addEventListener(AdobePSDK.PSDKEventType.AD_COMPLETED, onAdCompleted);
   
    <i>your_player</i>().addEventListener(AdobePSDK.PSDKEventType.AD_CLICKED, onAdClickedEvent);
   ```

1. Aggiungi gestori eventi.
a. Gestisci l’evento di inizio annuncio.
Questa operazione può comportare qualsiasi cosa, ad esempio la configurazione dell’interfaccia utente per l’utente.

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

   b. Gestisce l’evento su cui è stato fatto clic sull’annuncio.
In questo esempio, otteniamo informazioni sull’annuncio dall’evento e apriamo una nuova finestra del browser utilizzando tali informazioni:

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

   c. Gestisci l’evento di annuncio completato.

   ```
   onAdCompleted = function (event) { 
       if (clickAddButton) { 
           clickAddButton.setAttribute('hidden', 'true'); 
       } 
   }
   ```
