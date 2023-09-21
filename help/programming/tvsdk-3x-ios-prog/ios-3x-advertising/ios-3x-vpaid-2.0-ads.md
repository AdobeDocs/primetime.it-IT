---
description: Video Player Ad-Serving Interface Definition (VPAID) 2.0 offre un’interfaccia comune per la riproduzione di annunci video. Fornisce agli utenti un’esperienza multimediale avanzata e consente agli editori di eseguire meglio il targeting degli annunci, tracciare le impressioni degli annunci e monetizzare i contenuti video.
title: Supporto di annunci VPAID 2.0
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---

# Supporto di annunci VPAID 2.0 {#vpaid-ad-support}

Video Player Ad-Serving Interface Definition (VPAID) 2.0 offre un’interfaccia comune per la riproduzione di annunci video. Fornisce agli utenti un’esperienza multimediale avanzata e consente agli editori di eseguire meglio il targeting degli annunci, tracciare le impressioni degli annunci e monetizzare i contenuti video.

Sono supportate le seguenti funzionalità:

* Versione 2.0 delle specifiche VPAID

  Per ulteriori informazioni, consulta [IAB VPAID 2.0](https://www.iab.com/wp-content/uploads/2015/06/VPAID_2_0_Final_04-10-2012.pdf).
* Annunci VPAID lineari su contenuti video-on-demand (VOD)
* JavaScript per annunci VPAID

  Gli annunci VPAID devono essere basati su JavaScript e la risposta dell’annuncio deve identificare il tipo di file multimediale dell’annuncio VPAID come `application/javascript`.

Le seguenti funzioni non sono supportate:

* Versione 1.0 della specifica VPAID
* Annunci saltabili
* Annunci non lineari come annunci di sovrapposizione, annunci dinamici companion, annunci minimizzabili, annunci comprimibili e annunci espandibili
* Precaricamento di annunci VPAID
* Annunci VPAID nel contenuto live
* Flash annunci VPAID
* Annuncio VPAID post-roll

## Modifiche API {#section_D62F3E059C6C493592D34534B0BFC150}

Sono state apportate le seguenti modifiche all’API:

* `PTAuditudeMetadata` ha un `customAdLoadTimeout` per modificare il timeout predefinito nel processo di caricamento VPAID.

  Il valore di timeout predefinito è di 10 secondi.

* `PTMediaPlayerCustomAdNotification` viene inviato da `PTMediaPlayer` istanza

<!--<a id="section_495700E1C5404A7B85307A4137C740C5"></a>-->

Durante la riproduzione dell’annuncio VPAID:

* L’annuncio VPAID viene visualizzato in un contenitore di visualizzazione sopra la visualizzazione del lettore, pertanto il codice che si basa sulle digitazioni effettuate dagli utenti sulla visualizzazione del lettore non funziona.
* Il lettore di contenuti principale viene messo in pausa e chiama `pause` e `play` sull’istanza del lettore vengono utilizzati per mettere in pausa e riprendere l’annuncio VPAID.

* Gli annunci VPAID non hanno una durata predefinita, perché l’annuncio può essere interattivo.

  La durata dell’annuncio e la durata totale dell’interruzione pubblicitaria definite dalla risposta dell’ad server potrebbero non essere precise.

## Implementazione dell’integrazione VPAID 2.0 {#section_63C9C737367C4A0AB4D62E0DC2084141}

Per aggiungere il supporto VPAID 2.0 nell’applicazione iOS:

1. (Facoltativo) Aggiungi un listener per eventi annuncio personalizzati.

   ```
   [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerCustomAdNotification:) name:PTMediaPlayerCustomAdNotification object:self.player];
   ```

1. (Facoltativo) Visualizza la notifica.

   ```
   -(void)onMediaPlayerCustomAdNotification:(NSNotification *)notification{    PTCustomAdNotificationObject *notificationObject = [notification.userInfo objectForKey:PTCustomAdNotificationObjectKey];    if (notificationObject)    
   {        NSLog(@"ViewController:: Custom Ad Notification Received: %ld", notificationObject.type);    } 
   
   }
   ```
