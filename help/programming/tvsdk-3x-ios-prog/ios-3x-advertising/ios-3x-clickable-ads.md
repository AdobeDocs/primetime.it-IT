---
description: TVSDK fornisce informazioni utili per intervenire sugli annunci click-through. Quando crei la tua interfaccia utente del lettore, devi decidere come rispondere quando un utente fa clic su un annuncio cliccabile.
title: Annunci cliccabili
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---


# Annunci cliccabili {#clickable-ads}

TVSDK fornisce informazioni utili per intervenire sugli annunci click-through. Quando crei la tua interfaccia utente del lettore, devi decidere come rispondere quando un utente fa clic su un annuncio cliccabile.

In TVSDK per iOS, è possibile fare clic solo sugli annunci lineari.

## Rispondi ai clic sugli annunci {#section_537AF2593FDB4257B81AAE2103B0C719}

Quando un utente fa clic su un annuncio, su un annuncio pubblicitario correlato o su un pulsante correlato, l&#39;applicazione deve rispondere. TVSDK fornisce informazioni sull’URL di destinazione per il clic.

1. Per impostare un listener di eventi per TVSDK e fornire le informazioni sul click-through, aggiungi un osservatore per `PTMediaPlayerAdClickNotification`.

   >[!NOTE]
   >
   >Quando un utente fa clic su un annuncio, un annuncio pubblicitario correlato o un pulsante correlato, TVSDK invia questa notifica, incluse le informazioni sulla destinazione del clic.

1. Monitora le interazioni degli utenti sugli annunci cliccabili.
1. Quando l’utente tocca o fa clic sull’annuncio o sul pulsante, per inviare una notifica a TVSDK, utilizza `[_player notifyClick:_currentAd.primaryAsset];`.
1. Ascolta l’evento `PTMediaPlayerAdClickNotification` da TVSDK.
1. Per recuperare l’URL di click-through e le relative informazioni, utilizzare l’oggetto `PTMediaPlayerAdClickURLKey` .
1. Mette in pausa il video.
1. Utilizza le informazioni di click-through per visualizzare l’URL di click-through dell’annuncio e le relative informazioni.

   >[!NOTE]
   >
   >Ad esempio, puoi visualizzare le informazioni in uno dei seguenti modi:

   * Nell’applicazione aprendo l’URL di click-through in un browser.

      Sulle piattaforme desktop, l’area di riproduzione degli annunci video viene utilizzata per richiamare URL click-through ai clic dell’utente.
   * Reindirizza gli utenti al browser web per dispositivi mobili esterno.

      Sui dispositivi mobili, l’area di riproduzione degli annunci video viene utilizzata per altre funzioni, ad esempio per nascondere e visualizzare i controlli, mettere in pausa la riproduzione, espandere a schermo intero e così via. Su questi dispositivi viene utilizzata una visualizzazione separata, ad esempio un pulsante di sponsorizzazione, per avviare l’URL di click-through.

1. Chiudi la finestra del browser in cui vengono visualizzate le informazioni relative al click-through e riprende la riproduzione del video.

   Ad esempio:

   ```
      // Listening for click notification  
   [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerAdClick:)  
    name:PTMediaPlayerAdClickNotification object:self.player]; 
   - (void) onMediaPlayerAdClick:(NSNotification *) notification { 
      NSString *url = [notification.userInfo objectForKey:PTMediaPlayerAdClickURLKey];  
      if (url != nil) { 
          [self openBrowser:[NSURL URLWithString:url]]; 
      } 
   } 
   ```
