---
description: TVSDK fornisce informazioni che consentono di agire sugli annunci click-through. Quando crei l’interfaccia utente del lettore, devi decidere come rispondere quando un utente fa clic su un annuncio cliccabile.
title: Annunci cliccabili
exl-id: 4c4d37ee-0353-4c0f-8a11-d9be9bd427ec
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---

# Annunci cliccabili {#clickable-ads}

TVSDK fornisce informazioni che consentono di agire sugli annunci click-through. Quando crei l’interfaccia utente del lettore, devi decidere come rispondere quando un utente fa clic su un annuncio cliccabile.

In TVSDK per iOS, è possibile fare clic solo sugli annunci lineari.

## Rispondi ai clic sugli annunci {#section_537AF2593FDB4257B81AAE2103B0C719}

Quando un utente fa clic su un annuncio, un banner pubblicitario correlato o un pulsante correlato, l’applicazione deve rispondere. TVSDK fornisce informazioni sull’URL di destinazione del clic.

1. Per impostare un listener di eventi per TVSDK e fornire le informazioni di click-through, aggiungere un osservatore per `PTMediaPlayerAdClickNotification`.

   >[!NOTE]
   >
   >Quando un utente fa clic su un annuncio, su un banner pubblicitario correlato o su un pulsante correlato, TVSDK invia questa notifica, incluse le informazioni sulla destinazione del clic.

1. Monitora le interazioni degli utenti sugli annunci cliccabili.
1. Quando l’utente tocca o fa clic sull’annuncio o sul pulsante, per notificare TVSDK, utilizza `[_player notifyClick:_currentAd.primaryAsset];`.
1. Ascolta la `PTMediaPlayerAdClickNotification` da TVSDK.
1. Per recuperare l’URL di click-through e le informazioni correlate, utilizza `PTMediaPlayerAdClickURLKey` oggetto.
1. Metti in pausa il video.
1. Utilizza le informazioni di click-through per visualizzare l’URL di click-through dell’annuncio e le relative informazioni.

   >[!NOTE]
   >
   >Ad esempio, puoi visualizzare le informazioni in uno dei seguenti modi:

   * Nell’applicazione aprendo l’URL di click-through in un browser.

      Sulle piattaforme desktop, l’area di riproduzione degli annunci video viene utilizzata per richiamare gli URL di click-through ai clic dell’utente.
   * Reindirizza gli utenti al browser Web mobile esterno.

      Sui dispositivi mobili, l’area di riproduzione e il video vengono utilizzati per altre funzioni, ad esempio per nascondere e visualizzare i comandi, mettere in pausa la riproduzione, espandersi a schermo intero e così via. Su questi dispositivi, per avviare l’URL di click-through viene utilizzata una visualizzazione separata, ad esempio un pulsante di sponsor.

1. Chiudete la finestra del browser in cui vengono visualizzate le informazioni di click-through e riprendete la riproduzione del video.

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
