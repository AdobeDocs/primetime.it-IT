---
description: TVSDK fornisce informazioni utili per agire sugli annunci click-through. Durante la creazione dell’interfaccia utente del lettore, è necessario decidere come rispondere quando un utente fa clic su un annuncio selezionabile.
seo-description: TVSDK fornisce informazioni utili per agire sugli annunci click-through. Durante la creazione dell’interfaccia utente del lettore, è necessario decidere come rispondere quando un utente fa clic su un annuncio selezionabile.
seo-title: Annunci cliccabili
title: Annunci cliccabili
uuid: 8b257483-8b90-47cf-be2a-095b6d5b8883
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 0%

---


# Annunci cliccabili {#clickable-ads}

TVSDK fornisce informazioni utili per agire sugli annunci click-through. Durante la creazione dell’interfaccia utente del lettore, è necessario decidere come rispondere quando un utente fa clic su un annuncio selezionabile.

In TVSDK per iOS, è possibile fare clic solo sugli annunci lineari.

## Rispondi ai clic sugli annunci {#section_537AF2593FDB4257B81AAE2103B0C719}

Quando un utente fa clic su un annuncio, un banner pubblicitario complementare o un pulsante correlato, l&#39;applicazione deve rispondere. TVSDK fornisce informazioni sull’URL di destinazione per il clic.

1. Per impostare un listener di eventi per TVSDK e fornire le informazioni relative al click-through, aggiungere un osservatore per `PTMediaPlayerAdClickNotification`.

   >[!NOTE]
   >
   >Quando un utente fa clic su un annuncio, un banner pubblicitario complementare o un pulsante correlato, TVSDK invia la notifica, incluse le informazioni sulla destinazione del clic.

1. Monitora le interazioni degli utenti sugli annunci cliccabili.
1. Quando l&#39;utente tocca o fa clic sull&#39;annuncio o sul pulsante, per inviare una notifica a TVSDK, utilizza `[_player notifyClick:_currentAd.primaryAsset];`.
1. Ascoltare l&#39;evento `PTMediaPlayerAdClickNotification` da TVSDK.
1. Per recuperare l&#39;URL di click-through e le relative informazioni, utilizzare l&#39;oggetto `PTMediaPlayerAdClickURLKey`.
1. Metti in pausa il video.
1. Utilizzate le informazioni di click-through per visualizzare l&#39;URL di click-through dell&#39;annuncio e le relative informazioni.

   >[!NOTE]
   >
   >Ad esempio, potete visualizzare le informazioni in uno dei seguenti modi:

   * Nell’applicazione aprendo l’URL di click-through in un browser.

      Sulle piattaforme desktop, l’area di riproduzione dell’annuncio video viene utilizzata per richiamare gli URL di click-through ai clic dell’utente.
   * Reindirizzare gli utenti al browser Web esterno per dispositivi mobili.

      Sui dispositivi mobili, l’area di riproduzione video e video è utilizzata per altre funzioni, come nascondere e mostrare i controlli, mettere in pausa la riproduzione, espandere la visualizzazione a schermo intero e così via. Su questi dispositivi, per avviare l’URL di click-through viene utilizzata una visualizzazione separata, ad esempio un pulsante di sponsorizzazione.

1. Chiudete la finestra del browser in cui vengono visualizzate le informazioni di click-through e riavviate la riproduzione del video.

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
