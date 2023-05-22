---
description: Video Player Ad-Serving Interface Definition (VPAID) 2.0 offre un’interfaccia comune per la riproduzione di annunci video. Fornisce agli utenti un’esperienza multimediale avanzata e consente agli editori di eseguire meglio il targeting degli annunci, tracciare le impressioni degli annunci e monetizzare i contenuti video.
title: Supporto di annunci VPAID 2.0
exl-id: ee3e0cd9-463e-4de9-a94f-292e968b6f08
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '384'
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

## Modifiche API {#section_D62F3E059C6C493592D34534B0BFC150}

Sono state apportate le seguenti modifiche all’API:

* A `getCustomAdView` la funzione è stata aggiunta in `MediaPlayer` e restituisce la visualizzazione web che esegue il rendering dell’annuncio VPAID.

   Per ulteriori informazioni su `CustomAdView` oggetto restituito da questa funzione, vedere [Riferimenti API](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/index.html).

* A `CUSTOM_AD` viene inviato dall’istanza del lettore multimediale.

   L&#39;applicazione può registrare un callback di evento implementando `CustomAdEventListener`.

* `MediaPlayer.setCustomAdTimeout(int milliseconds)` consente di modificare il timeout predefinito nel processo di caricamento VPAID.

   Il valore di timeout predefinito è di 10 secondi.

<!--<a id="section_495700E1C5404A7B85307A4137C740C5"></a>-->

Durante la riproduzione dell’annuncio VPAID:

* L’annuncio VPAID viene visualizzato in un contenitore di visualizzazione sopra la visualizzazione del lettore, pertanto il codice che si basa sulle digitazioni effettuate dagli utenti sulla visualizzazione del lettore non funziona.
* Il lettore di contenuti principale viene messo in pausa e chiama `pause` e `play` sull’istanza del lettore vengono utilizzati per mettere in pausa e riprendere l’annuncio VPAID.

* Gli annunci VPAID non hanno una durata predefinita, perché l’annuncio può essere interattivo.

   La durata dell’annuncio e la durata totale dell’interruzione pubblicitaria definite dalla risposta dell’ad server potrebbero non essere precise.

## Implementazione dell’integrazione VPAID 2.0 {#implement-vpaid-integration}

Per aggiungere il supporto VPAID 2.0, aggiungi una visualizzazione annuncio personalizzata e i listener appropriati.

Per aggiungere il supporto VPAID 2.0:

1. Aggiungi la visualizzazione annuncio personalizzata all’interfaccia del lettore.

   ```java
   _playerFrame.addView(mediaPlayer.createCustomAdView());
   ```

1. Aggiungi un listener per gli eventi annuncio personalizzati.

   ```java
   mediaplayer.addEventListener(MediaPlayer.Event.CUSTOM_AD,  
     _customAdEventListener);
   ```
