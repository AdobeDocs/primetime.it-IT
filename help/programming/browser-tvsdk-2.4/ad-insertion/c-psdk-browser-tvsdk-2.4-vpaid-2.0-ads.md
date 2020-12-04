---
description: La definizione dell'interfaccia ad-serving del lettore video (VPAID) 2.0 fornisce un'interfaccia comune per la riproduzione di annunci video. Offre agli utenti un’esperienza multimediale completa e consente agli editori di eseguire il targeting degli annunci, tenere traccia delle impressioni degli annunci e monetizzare i contenuti video.
seo-description: La definizione dell'interfaccia ad-serving del lettore video (VPAID) 2.0 fornisce un'interfaccia comune per la riproduzione di annunci video. Offre agli utenti un’esperienza multimediale completa e consente agli editori di eseguire il targeting degli annunci, tenere traccia delle impressioni degli annunci e monetizzare i contenuti video.
seo-title: Supporto per VPAID 2.0 ad
title: Supporto per VPAID 2.0 ad
uuid: 462692b5-c4b3-4488-adb3-f309809d64ad
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---


# Supporto di annunci VPAID 2.0 {#vpaid-ad-support}

La definizione dell&#39;interfaccia ad-serving del lettore video (VPAID) 2.0 fornisce un&#39;interfaccia comune per la riproduzione di annunci video. Offre agli utenti un’esperienza multimediale completa e consente agli editori di eseguire il targeting degli annunci, tenere traccia delle impressioni degli annunci e monetizzare i contenuti video.

Sono supportate le seguenti funzionalità:

* Versione 2.0 della specifica VPAID

   Per ulteriori informazioni, vedere [IAB VPAID 2.0](https://www.iab.com/guidelines/digital-video-player-ad-interface-definition-vpaid-2-0/).
* Annunci VPAID lineari con contenuti video su richiesta (VOD)
* Nel contenuto live, l&#39;SDK per browser supporta gli annunci VPAID JavaScript pre-roll.
* In modalità di fallback del Flash, il browser TVSDK supporta solo gli annunci VPAID basati su Flash.
* Annunci VPAID JavaScript lineari

   Gli annunci VPAID devono essere basati su JavaScript e la risposta dell&#39;annuncio deve identificare il tipo di supporto dell&#39;annuncio VPAID come `application/javascript`.

Le seguenti funzionalità non sono supportate:

* Versione 1.0 della specifica VPAID
* Annunci Skippable
* Annunci non lineari, come annunci overlay, annunci companion dinamici, annunci minimizable, annunci compressi e annunci espandibili.
* Precaricamento degli annunci VPAID
* Annunci VPAID nel contenuto live
* Annunci VPAID Flash

## API {#section_0DB1D383CA5047B281BC808BC082C69B}

I seguenti elementi API supportano gli annunci VPAID 2.0:

* Il metodo `getCustomAdView` di `MediaPlayer` restituisce un oggetto `CustomAdView` che rappresenta la visualizzazione Web che esegue il rendering dell&#39;annuncio VPAID.

   Per ulteriori informazioni sul metodo `getCustomAdView`, consultare la sezione [Documentazione API di MediaPlayer](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/AdobePSDK.MediaPlayer.html).

* `MediaPlayer.setCustomAdTimeout(int milliseconds)` imposta il timeout sul processo di caricamento VPAID.

   Il valore di timeout predefinito è 10 secondi.

* L&#39;API `auditudeSettings.ignoreVPAIDAds` consente di ignorare gli annunci VPAID ricevuti dal server Auditude. L&#39;API non funziona per Fallback Flash.

Durante la riproduzione dell&#39;annuncio VPAID:

* L&#39;annuncio VPAID viene visualizzato in un contenitore di viste sopra la vista del lettore, pertanto il codice che si basa sui tocchi degli utenti sulla vista del lettore non funziona.
* Le chiamate per mettere in pausa e riprodurre l&#39;istanza del lettore mettono in pausa e riprendono l&#39;annuncio VPAID.
* Gli annunci VPAID non hanno una durata predefinita, perché l&#39;annuncio può essere interattivo.

   La durata dell&#39;annuncio e la durata totale dell&#39;interruzione dell&#39;annuncio, specificate nella risposta del server dell&#39;annuncio, potrebbero non essere precise.