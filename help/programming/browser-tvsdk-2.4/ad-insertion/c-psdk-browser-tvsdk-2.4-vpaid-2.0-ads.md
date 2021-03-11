---
description: La definizione dell'interfaccia di ad-serving del lettore video (VPAID) 2.0 fornisce un'interfaccia comune per la riproduzione di annunci video. Offre agli utenti un’esperienza multimediale avanzata e consente agli editori di eseguire meglio il targeting degli annunci, tenere traccia delle impressioni degli annunci e monetizzare i contenuti video.
title: Supporto per annunci VPAID 2.0
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---


# Supporto per annunci VPAID 2.0 {#vpaid-ad-support}

La definizione dell&#39;interfaccia di ad-serving del lettore video (VPAID) 2.0 fornisce un&#39;interfaccia comune per la riproduzione di annunci video. Offre agli utenti un’esperienza multimediale avanzata e consente agli editori di eseguire meglio il targeting degli annunci, tenere traccia delle impressioni degli annunci e monetizzare i contenuti video.

Sono supportate le seguenti funzioni:

* Versione 2.0 della specifica VPAID

   Per ulteriori informazioni, consulta [IAB VPAID 2.0](https://www.iab.com/guidelines/digital-video-player-ad-interface-definition-vpaid-2-0/).
* Annunci VPAID lineari con contenuti video on demand (VOD)
* Nel contenuto live, il browser TVSDK supporta gli annunci VPAID pre-roll JavaScript.
* In modalità di fallback del Flash, il browser TVSDK supporta solo annunci VPAID basati sul Flash.
* Annunci VPAID JavaScript lineari

   Gli annunci VPAID devono essere basati su JavaScript e la risposta dell&#39;annuncio deve identificare il tipo di supporto dell&#39;annuncio VPAID come `application/javascript`.

Le seguenti funzionalità non sono supportate:

* Versione 1.0 della specifica VPAID
* Annunci copiosi
* Annunci non lineari, come annunci sovrapposti, annunci dinamici complementari, annunci minimizzabili, annunci compressi e annunci espandibili.
* Precaricamento degli annunci VPAID
* Annunci VPAID nel contenuto live
* Annunci VPAID Flash

## API {#section_0DB1D383CA5047B281BC808BC082C69B}

I seguenti elementi API supportano gli annunci VPAID 2.0:

* Il metodo `getCustomAdView` di `MediaPlayer` restituisce un oggetto `CustomAdView` che rappresenta la visualizzazione web che esegue il rendering dell&#39;annuncio VPAID.

   Per ulteriori informazioni sul metodo `getCustomAdView`, consulta la [documentazione API MediaPlayer](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/AdobePSDK.MediaPlayer.html).

* `MediaPlayer.setCustomAdTimeout(int milliseconds)` imposta il timeout sul processo di caricamento VPAID.

   Il valore di timeout predefinito è 10 secondi.

* L’API `auditudeSettings.ignoreVPAIDAds` ti consente di ignorare gli annunci VPAID ricevuti dal server Auditude. L’API non funziona per Fallback di Flash.

Durante la riproduzione dell’annuncio VPAID:

* L&#39;annuncio VPAID viene visualizzato in un contenitore di visualizzazione sopra la visualizzazione del lettore, pertanto il codice che si basa sui tocco degli utenti sulla visualizzazione del lettore non funziona.
* Le chiamate per mettere in pausa e riprodurre l&#39;istanza del lettore mettono in pausa e riprendono l&#39;annuncio VPAID.
* Gli annunci VPAID non hanno una durata predefinita, perché l&#39;annuncio può essere interattivo.

   La durata dell&#39;annuncio e la durata totale dell&#39;interruzione dell&#39;annuncio specificati nella risposta del server dell&#39;annuncio potrebbero non essere precise.