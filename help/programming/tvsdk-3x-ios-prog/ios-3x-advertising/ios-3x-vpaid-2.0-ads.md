---
description: Video Player Ad-Serving Interface Definition (VPAID) 2.0 fornisce un'interfaccia comune per riprodurre annunci video. Offre agli utenti un’esperienza multimediale completa e consente agli editori di eseguire il targeting degli annunci, tenere traccia delle impressioni degli annunci e monetizzare i contenuti video.
seo-description: Video Player Ad-Serving Interface Definition (VPAID) 2.0 fornisce un'interfaccia comune per riprodurre annunci video. Offre agli utenti un’esperienza multimediale completa e consente agli editori di eseguire il targeting degli annunci, tenere traccia delle impressioni degli annunci e monetizzare i contenuti video.
seo-title: Supporto per VPAID 2.0 ad
title: Supporto per VPAID 2.0 ad
uuid: b688d244-c5ac-4832-b5c2-cb25bc80ce8b
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---


# Supporto di annunci VPAID 2.0 {#vpaid-ad-support}

Video Player Ad-Serving Interface Definition (VPAID) 2.0 fornisce un&#39;interfaccia comune per riprodurre annunci video. Offre agli utenti un’esperienza multimediale completa e consente agli editori di eseguire il targeting degli annunci, tenere traccia delle impressioni degli annunci e monetizzare i contenuti video.

Sono supportate le seguenti funzionalità:

* Versione 2.0 della specifica VPAID

   Per ulteriori informazioni, fare riferimento a [IAB VPAID 2.0](https://www.iab.com/wp-content/uploads/2015/06/VPAID_2_0_Final_04-10-2012.pdf).
* Annunci VPAID lineari su contenuti video su richiesta (VOD)
* Annunci VPAID JavaScript

   Gli annunci VPAID devono essere basati su JavaScript e la risposta dell&#39;annuncio deve identificare il tipo di supporto dell&#39;annuncio VPAID come `application/javascript`.

Le seguenti funzionalità non sono supportate:

* Versione 1.0 della specifica VPAID
* Annunci Skippable
* Annunci non lineari come annunci overlay, annunci companistici dinamici, annunci minimizzabili, annunci compressi e annunci espandibili
* Precaricamento degli annunci VPAID
* Annunci VPAID nel contenuto live
* Annunci VPAID Flash
* Annuncio VPAID post-roll

## Modifiche API {#section_D62F3E059C6C493592D34534B0BFC150}

Sono state apportate le seguenti modifiche all&#39;API:

* `PTAuditudeMetadata` dispone di una  `customAdLoadTimeout` proprietà per modificare il timeout predefinito nel processo di caricamento VPAID.

   Il valore di timeout predefinito è 10 secondi.

* `PTMediaPlayerCustomAdNotification` viene inviato dall&#39; `PTMediaPlayer` istanza

<!--<a id="section_495700E1C5404A7B85307A4137C740C5"></a>-->

Durante la riproduzione dell&#39;annuncio VPAID:

* L&#39;annuncio VPAID viene visualizzato in un contenitore di visualizzazione sopra la vista del lettore, in modo che il codice che si basa sui tocchi degli utenti nella vista del lettore non funzioni.
* Il lettore del contenuto principale viene messo in pausa e le chiamate a `pause` e `play` nell&#39;istanza del lettore vengono utilizzate per mettere in pausa e riprendere l&#39;annuncio VPAID.

* Gli annunci VPAID non hanno una durata predefinita, perché l&#39;annuncio può essere interattivo.

   La durata dell&#39;annuncio e la durata totale dell&#39;interruzione dell&#39;annuncio, definite dalla risposta del server dell&#39;annuncio, potrebbero non essere precise.

## Implementare l&#39;integrazione VPAID 2.0 {#section_63C9C737367C4A0AB4D62E0DC2084141}

Per aggiungere il supporto VPAID 2.0 nell&#39;applicazione iOS:

1. (Facoltativo) Aggiungere un listener per gli eventi di annunci personalizzati.

   ```
   [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerCustomAdNotification:) name:PTMediaPlayerCustomAdNotification object:self.player];
   ```

1. (Facoltativo) Visualizzare la notifica.

   ```
   -(void)onMediaPlayerCustomAdNotification:(NSNotification *)notification{    PTCustomAdNotificationObject *notificationObject = [notification.userInfo objectForKey:PTCustomAdNotificationObjectKey];    if (notificationObject)    
   {        NSLog(@"ViewController:: Custom Ad Notification Received: %ld", notificationObject.type);    } 
   
   }
   ```
