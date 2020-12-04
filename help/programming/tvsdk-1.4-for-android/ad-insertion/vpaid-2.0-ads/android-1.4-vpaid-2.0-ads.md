---
description: Video Player Ad-Serving Interface Definition (VPAID) 2.0 fornisce un'interfaccia comune per riprodurre annunci video. Offre agli utenti un’esperienza multimediale completa e consente agli editori di eseguire il targeting degli annunci, tenere traccia delle impressioni degli annunci e monetizzare i contenuti video.
seo-description: Video Player Ad-Serving Interface Definition (VPAID) 2.0 fornisce un'interfaccia comune per riprodurre annunci video. Offre agli utenti un’esperienza multimediale completa e consente agli editori di eseguire il targeting degli annunci, tenere traccia delle impressioni degli annunci e monetizzare i contenuti video.
seo-title: Supporto per VPAID 2.0 ad
title: Supporto per VPAID 2.0 ad
uuid: 7168a6e4-9c5e-4d3a-8710-867cf98e4445
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '423'
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

## Modifiche API {#section_D62F3E059C6C493592D34534B0BFC150}

Sono state apportate le seguenti modifiche all&#39;API:

* È stata aggiunta una funzione `getCustomAdView` in `MediaPlayer` e restituisce la visualizzazione Web che esegue il rendering dell&#39;annuncio VPAID.

   Per ulteriori informazioni sull&#39;oggetto `CustomAdView` restituito da questa funzione, vedere [Riferimenti API](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/index.html).

* Un evento `CUSTOM_AD` viene inviato dall&#39;istanza del lettore multimediale.

   L&#39;applicazione può registrare un callback di evento implementando `CustomAdEventListener`.

* `MediaPlayer.setCustomAdTimeout(int milliseconds)` consente di modificare il timeout predefinito nel processo di caricamento VPAID.

   Il valore di timeout predefinito è 10 secondi.

<!--<a id="section_495700E1C5404A7B85307A4137C740C5"></a>-->

Durante la riproduzione dell&#39;annuncio VPAID:

* L&#39;annuncio VPAID viene visualizzato in un contenitore di visualizzazione sopra la vista del lettore, in modo che il codice che si basa sui tocchi degli utenti nella vista del lettore non funzioni.
* Il lettore del contenuto principale viene messo in pausa e le chiamate a `pause` e `play` nell&#39;istanza del lettore vengono utilizzate per mettere in pausa e riprendere l&#39;annuncio VPAID.

* Gli annunci VPAID non hanno una durata predefinita, perché l&#39;annuncio può essere interattivo.

   La durata dell&#39;annuncio e la durata totale dell&#39;interruzione dell&#39;annuncio, definite dalla risposta del server dell&#39;annuncio, potrebbero non essere precise.

## Implementare l&#39;integrazione VPAID 2.0 {#implement-vpaid-integration}

Per aggiungere il supporto VPAID 2.0, aggiungi una visualizzazione ad personalizzata e i listener appropriati.

Per aggiungere il supporto VPAID 2.0:

1. Aggiungere la visualizzazione annunci personalizzata all&#39;interfaccia del lettore.

   ```java
   _playerFrame.addView(mediaPlayer.createCustomAdView());
   ```

1. Aggiunta di un listener per gli eventi di annunci personalizzati.

   ```java
   mediaplayer.addEventListener(MediaPlayer.Event.CUSTOM_AD,  
     _customAdEventListener);
   ```
