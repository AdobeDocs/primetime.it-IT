---
description: Video Player Ad-Serving Interface Definition (VPAID) 2.0 fornisce un'interfaccia comune per riprodurre annunci video. Offre agli utenti un’esperienza multimediale avanzata e consente agli editori di eseguire meglio il targeting degli annunci, tenere traccia delle impressioni degli annunci e monetizzare i contenuti video.
title: Supporto per annunci VPAID 2.0
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---


# Supporto per annunci VPAID 2.0 {#vpaid-ad-support}

Video Player Ad-Serving Interface Definition (VPAID) 2.0 fornisce un&#39;interfaccia comune per riprodurre annunci video. Offre agli utenti un’esperienza multimediale avanzata e consente agli editori di eseguire meglio il targeting degli annunci, tenere traccia delle impressioni degli annunci e monetizzare i contenuti video.

Sono supportate le seguenti funzioni:

* Versione 2.0 della specifica VPAID

   Per ulteriori informazioni, consulta [IAB VPAID 2.0](https://www.iab.com/wp-content/uploads/2015/06/VPAID_2_0_Final_04-10-2012.pdf).
* Annunci VPAID lineari su contenuti video on demand (VOD)
* Annunci VPAID JavaScript

   Gli annunci VPAID devono essere basati su JavaScript e la risposta dell&#39;annuncio deve identificare il tipo di supporto dell&#39;annuncio VPAID come `application/javascript`.

Le seguenti funzionalità non sono supportate:

* Versione 1.0 della specifica VPAID
* Annunci copiosi
* Annunci non lineari come annunci di sovrapposizione, annunci dinamici di accompagnamento, annunci minimizzabili, annunci comprimibili e annunci espandibili
* Precaricamento degli annunci VPAID
* Annunci VPAID nel contenuto live
* Annunci VPAID Flash
* annuncio VPAID post-roll

## Modifiche API {#section_D62F3E059C6C493592D34534B0BFC150}

Sono state apportate le seguenti modifiche all’API:

* `PTAuditudeMetadata` dispone di una  `customAdLoadTimeout` proprietà per modificare il timeout predefinito nel processo di caricamento VPAID.

   Il valore di timeout predefinito è 10 secondi.

* `PTMediaPlayerCustomAdNotification` viene inviato dall&#39; `PTMediaPlayer` istanza

<!--<a id="section_495700E1C5404A7B85307A4137C740C5"></a>-->

Durante la riproduzione dell’annuncio VPAID:

* L’annuncio VPAID viene visualizzato in un contenitore di visualizzazione sopra la visualizzazione del lettore, in modo che il codice che si basa sui tocco degli utenti sulla visualizzazione del lettore non funzioni.
* Il lettore di contenuti principale viene messo in pausa e le chiamate a `pause` e `play` sull&#39;istanza del lettore vengono utilizzate per mettere in pausa e riprendere l&#39;annuncio VPAID.

* Gli annunci VPAID non hanno una durata predefinita, perché l&#39;annuncio può essere interattivo.

   La durata dell&#39;annuncio e la durata totale dell&#39;interruzione dell&#39;annuncio definita dalla risposta del server dell&#39;annuncio potrebbero non essere precise.

## Implementare l&#39;integrazione VPAID 2.0 {#section_63C9C737367C4A0AB4D62E0DC2084141}

Per aggiungere il supporto VPAID 2.0 nella tua applicazione iOS:

1. (Facoltativo) Aggiungi un listener per gli eventi di annunci personalizzati.

   ```
   [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerCustomAdNotification:) name:PTMediaPlayerCustomAdNotification object:self.player];
   ```

1. (Facoltativo) Visualizza la notifica.

   ```
   -(void)onMediaPlayerCustomAdNotification:(NSNotification *)notification{    PTCustomAdNotificationObject *notificationObject = [notification.userInfo objectForKey:PTCustomAdNotificationObjectKey];    if (notificationObject)    
   {        NSLog(@"ViewController:: Custom Ad Notification Received: %ld", notificationObject.type);    } 
   
   }
   ```

