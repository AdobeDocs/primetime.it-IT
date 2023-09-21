---
description: Il lettore video ad-serving interface definition (VPAID) 2.0 offre un’interfaccia comune per la riproduzione di annunci video. Fornisce agli utenti un’esperienza multimediale avanzata e consente agli editori di eseguire meglio il targeting degli annunci, tracciare le impressioni degli annunci e monetizzare i contenuti video.
title: Supporto di annunci VPAID 2.0
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---

# Supporto di annunci VPAID 2.0 {#vpaid-ad-support}

Il lettore video ad-serving interface definition (VPAID) 2.0 offre un’interfaccia comune per la riproduzione di annunci video. Fornisce agli utenti un’esperienza multimediale avanzata e consente agli editori di eseguire meglio il targeting degli annunci, tracciare le impressioni degli annunci e monetizzare i contenuti video.

Sono supportate le seguenti funzionalità:

* Versione 2.0 delle specifiche VPAID

  Per ulteriori informazioni, consulta [IAB VPAID 2.0](https://www.iab.com/wp-content/uploads/2015/06/VPAID_2_0_Final_04-10-2012.pdf).
* Annunci VPAID lineari con contenuto video-on-demand (VOD)
* JavaScript per annunci VPAID

  Gli annunci VPAID devono essere basati su JavaScript e la risposta dell’annuncio deve identificare il tipo di file multimediale dell’annuncio VPAID come `application/javascript`.

Le seguenti funzioni non sono supportate:

* Versione 1.0 della specifica VPAID
* Annunci saltabili
* Annunci non lineari, come annunci sovrapposti, annunci dinamici di accompagnamento, annunci minimizzabili, annunci comprimibili e annunci espandibili
* Precaricamento di annunci VPAID
* Annunci VPAID nel contenuto live
* Flash annunci VPAID

## API

I seguenti elementi API supportano gli annunci VPAID 2.0:

* Il `getCustomAdView` metodo di `MediaPlayer` restituisce un `CustomAdView` , che rappresenta la visualizzazione web che esegue il rendering dell&#39;annuncio VPAID (vedere [Riferimenti API](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/index.html)).

* `MediaPlayer.setCustomAdTimeout(int milliseconds)` imposta il timeout del processo di caricamento VPAID. Il valore di timeout predefinito è di 10 secondi.

Durante la riproduzione dell’annuncio VPAID:

* L’annuncio VPAID viene visualizzato in un contenitore di viste sopra la vista del lettore, pertanto non funziona il codice che si basa sulle digitazioni effettuate dagli utenti sulla vista del lettore.
* Chiamate a `pause` e `play` sull’istanza del lettore, sospendi e riprendi l’annuncio VPAID.

* Gli annunci VPAID non hanno una durata predefinita, perché l’annuncio può essere interattivo.

  La durata dell’annuncio e la durata totale dell’interruzione pubblicitaria specificate nella risposta dell’ad server potrebbero non essere precise.
