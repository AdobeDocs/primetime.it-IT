---
description: Il lettore video ad-serving interface definition (VPAID) 2.0 offre un’interfaccia comune per la riproduzione di annunci video. Fornisce agli utenti un’esperienza multimediale avanzata e consente agli editori di eseguire meglio il targeting degli annunci, tracciare le impressioni degli annunci e monetizzare i contenuti video.
title: Supporto di annunci VPAID 2.0
exl-id: ea3dcd1d-c4e2-46c6-b613-e86c3e161ca8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---

# Supporto di annunci VPAID 2.0 {#vpaid-ad-support}

Il lettore video ad-serving interface definition (VPAID) 2.0 offre un’interfaccia comune per la riproduzione di annunci video. Fornisce agli utenti un’esperienza multimediale avanzata e consente agli editori di eseguire meglio il targeting degli annunci, tracciare le impressioni degli annunci e monetizzare i contenuti video.

Sono supportate le seguenti funzionalità:

* Versione 2.0 delle specifiche VPAID

   Per ulteriori informazioni, consulta [IAB VPAID 2.0](https://www.iab.com/guidelines/digital-video-player-ad-interface-definition-vpaid-2-0/).
* Annunci VPAID lineari con contenuto video-on-demand (VOD)
* Nel contenuto Live, il browser TVSDK supporta gli annunci VPAID JavaScript pre-roll.
* In modalità di fallback del Flash, l’SDK del browser supporta solo gli annunci VPAID basati sul Flash.
* Annunci VPAID JavaScript lineari

   Gli annunci VPAID devono essere basati su JavaScript e la risposta dell’annuncio deve identificare il tipo di file multimediale dell’annuncio VPAID come `application/javascript`.

Le seguenti funzioni non sono supportate:

* Versione 1.0 della specifica VPAID
* Annunci saltabili
* Annunci non lineari, come annunci sovrapposti, annunci dinamici di accompagnamento, annunci minimizzabili, annunci comprimibili e annunci espandibili.
* Precaricamento di annunci VPAID
* Annunci VPAID nel contenuto live
* Flash annunci VPAID

## API {#section_0DB1D383CA5047B281BC808BC082C69B}

I seguenti elementi API supportano gli annunci VPAID 2.0:

* Il `getCustomAdView` metodo di `MediaPlayer` restituisce un `CustomAdView` oggetto, che rappresenta la visualizzazione web che esegue il rendering dell’annuncio VPAID.

   Per ulteriori informazioni su `getCustomAdView` metodo, vedi [Documentazione API di MediaPlayer](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/AdobePSDK.MediaPlayer.html).

* `MediaPlayer.setCustomAdTimeout(int milliseconds)` imposta il timeout del processo di caricamento VPAID.

   Il valore di timeout predefinito è di 10 secondi.

* API, `auditudeSettings.ignoreVPAIDAds`, consente di ignorare gli annunci VPAID ricevuti dal server Auditude. L’API non funziona per il fallback del Flash.

Durante la riproduzione dell’annuncio VPAID:

* L’annuncio VPAID viene visualizzato in un contenitore di viste sopra la vista del lettore, pertanto non funziona il codice che si basa sulle digitazioni effettuate dagli utenti sulla vista del lettore.
* Chiamate per la pausa e la riproduzione sull&#39;istanza del lettore pausa e ripresa dell&#39;annuncio VPAID.
* Gli annunci VPAID non hanno una durata predefinita, perché l’annuncio può essere interattivo.

   La durata dell’annuncio e la durata totale dell’interruzione pubblicitaria specificate nella risposta dell’ad server potrebbero non essere precise.
