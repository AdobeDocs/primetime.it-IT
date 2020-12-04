---
description: La definizione dell'interfaccia ad-serving del lettore video (VPAID) 2.0 fornisce un'interfaccia comune per la riproduzione di annunci video. Offre agli utenti un’esperienza multimediale completa e consente agli editori di eseguire il targeting degli annunci, tenere traccia delle impressioni degli annunci e monetizzare i contenuti video.
seo-description: La definizione dell'interfaccia ad-serving del lettore video (VPAID) 2.0 fornisce un'interfaccia comune per la riproduzione di annunci video. Offre agli utenti un’esperienza multimediale completa e consente agli editori di eseguire il targeting degli annunci, tenere traccia delle impressioni degli annunci e monetizzare i contenuti video.
seo-title: Supporto per VPAID 2.0 ad
title: Supporto per VPAID 2.0 ad
uuid: e45e91d2-2aef-4d69-ac80-228d23e8fd7b
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---


# Panoramica {#vpaid-ad-support-overview}

La definizione dell&#39;interfaccia ad-serving del lettore video (VPAID) 2.0 fornisce un&#39;interfaccia comune per la riproduzione di annunci video. Offre agli utenti un’esperienza multimediale completa e consente agli editori di eseguire il targeting degli annunci, tenere traccia delle impressioni degli annunci e monetizzare i contenuti video.

Sono supportate le seguenti funzionalità:

* Versione 2.0 della specifica VPAID

   Per ulteriori informazioni, fare riferimento a [IAB VPAID 2.0](https://www.iab.com/wp-content/uploads/2015/06/VPAID_2_0_Final_04-10-2012.pdf).
* Annunci VPAID lineari con contenuti video su richiesta (VOD)
* Annunci VPAID JavaScript

   Gli annunci VPAID devono essere basati su JavaScript e la risposta dell&#39;annuncio deve identificare il tipo di supporto dell&#39;annuncio VPAID come `application/javascript`.

Le seguenti funzionalità non sono supportate:

* Versione 1.0 della specifica VPAID
* Annunci Skippable
* Annunci non lineari, come annunci di sovrapposizione, annunci di accompagnamento dinamici, annunci ridotti a icona, annunci compressi e annunci espandibili
* Precaricamento degli annunci VPAID
* Annunci VPAID nel contenuto live
* Annunci VPAID Flash

## API

I seguenti elementi API supportano gli annunci VPAID 2.0:

* Il metodo `getCustomAdView` di `MediaPlayer` restituisce un oggetto `CustomAdView` che rappresenta la visualizzazione Web che esegue il rendering dell&#39;annuncio VPAID (vedere [Riferimenti API](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/index.html)).

* `MediaPlayer.setCustomAdTimeout(int milliseconds)` imposta il timeout sul processo di caricamento VPAID. Il valore di timeout predefinito è 10 secondi.

Durante la riproduzione dell&#39;annuncio VPAID:

* L&#39;annuncio VPAID viene visualizzato in un contenitore di viste sopra la vista del lettore, pertanto il codice che si basa sui tocchi degli utenti sulla vista del lettore non funziona.
* Le chiamate a `pause` e `play` sull&#39;istanza del lettore mettono in pausa e riprendono l&#39;annuncio VPAID.

* Gli annunci VPAID non hanno una durata predefinita, perché l&#39;annuncio può essere interattivo.

   La durata dell&#39;annuncio e la durata totale dell&#39;interruzione dell&#39;annuncio, specificate nella risposta del server dell&#39;annuncio, potrebbero non essere precise.