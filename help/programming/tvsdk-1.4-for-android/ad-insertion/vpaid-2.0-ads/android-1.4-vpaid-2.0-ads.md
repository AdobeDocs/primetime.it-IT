---
description: Video Player Ad-Serving Interface Definition (VPAID) 2.0 fornisce un'interfaccia comune per riprodurre annunci video. Offre agli utenti un’esperienza multimediale avanzata e consente agli editori di eseguire meglio il targeting degli annunci, tenere traccia delle impressioni degli annunci e monetizzare i contenuti video.
title: Supporto per annunci VPAID 2.0
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '384'
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

## Modifiche API {#section_D62F3E059C6C493592D34534B0BFC150}

Sono state apportate le seguenti modifiche all’API:

* È stata aggiunta una funzione `getCustomAdView` in `MediaPlayer` e restituisce la visualizzazione Web che esegue il rendering dell’annuncio VPAID.

   Per ulteriori informazioni sull&#39;oggetto `CustomAdView` restituito da questa funzione, vedere [Riferimenti API](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/index.html).

* Un evento `CUSTOM_AD` viene inviato dall&#39;istanza del lettore multimediale.

   L&#39;applicazione può registrare un callback di un evento implementando `CustomAdEventListener`.

* `MediaPlayer.setCustomAdTimeout(int milliseconds)` consente di modificare il timeout predefinito nel processo di caricamento VPAID.

   Il valore di timeout predefinito è 10 secondi.

<!--<a id="section_495700E1C5404A7B85307A4137C740C5"></a>-->

Durante la riproduzione dell’annuncio VPAID:

* L’annuncio VPAID viene visualizzato in un contenitore di visualizzazione sopra la visualizzazione del lettore, in modo che il codice che si basa sui tocco degli utenti sulla visualizzazione del lettore non funzioni.
* Il lettore di contenuti principale viene messo in pausa e le chiamate a `pause` e `play` sull&#39;istanza del lettore vengono utilizzate per mettere in pausa e riprendere l&#39;annuncio VPAID.

* Gli annunci VPAID non hanno una durata predefinita, perché l&#39;annuncio può essere interattivo.

   La durata dell&#39;annuncio e la durata totale dell&#39;interruzione dell&#39;annuncio definita dalla risposta del server dell&#39;annuncio potrebbero non essere precise.

## Implementare l&#39;integrazione VPAID 2.0 {#implement-vpaid-integration}

Per aggiungere il supporto VPAID 2.0, aggiungi una visualizzazione annunci personalizzata e gli ascoltatori appropriati.

Per aggiungere il supporto VPAID 2.0:

1. Aggiungi la visualizzazione annunci personalizzata all’interfaccia del lettore.

   ```java
   _playerFrame.addView(mediaPlayer.createCustomAdView());
   ```

1. Aggiungi un listener per gli eventi di annunci personalizzati.

   ```java
   mediaplayer.addEventListener(MediaPlayer.Event.CUSTOM_AD,  
     _customAdEventListener);
   ```
