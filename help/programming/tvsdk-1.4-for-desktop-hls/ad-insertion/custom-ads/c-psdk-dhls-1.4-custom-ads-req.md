---
description: La definizione VPAID (Video Player Ad-Serving Interface Definition) fornisce un’interfaccia comune per la riproduzione di annunci video. VPAID offre agli utenti un’esperienza multimediale avanzata e consente agli editori di eseguire meglio il targeting degli annunci, tenere traccia delle impression pubblicitarie e monetizzare i contenuti video.
title: Requisiti degli annunci personalizzati
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# Requisiti degli annunci personalizzati {#custom-ad-requirements}

Il lettore TVSDK può riprodurre annunci digitali di Ad-Interface Definition (VPAID) per lettore video e visualizzare lo stato di caricamento dell’annuncio. Se nell’annuncio sono presenti errori o il caricamento degli annunci richiede troppo tempo, TVSDK ignora questi annunci.

La definizione VPAID (Video Player Ad-Serving Interface Definition) fornisce un’interfaccia comune per la riproduzione di annunci video. VPAID offre agli utenti un’esperienza multimediale avanzata e consente agli editori di eseguire meglio il targeting degli annunci, tenere traccia delle impression pubblicitarie e monetizzare i contenuti video.

<!--<a id="section_9A358902CBC24999BA34206EE2029616"></a>-->

TVSDK supporta le seguenti funzionalità:

* Versione 1.0 e 2.0 della specifica VPAID
* Annunci VPAID lineari su contenuti video-on-demand (VOD)
* Flash annunci VPAID

  Gli annunci VPAID devono essere basati su Flash e la risposta dell’annuncio deve identificare il tipo di file multimediale dell’annuncio VPAID come `application/x-shockwave-flash`.

Le seguenti funzioni non sono supportate:

* Annunci non lineari come annunci di sovrapposizione e annunci dinamici companion
* Precaricamento di annunci VPAID
* Annunci VPAID nel contenuto live
* JavaScript per annunci VPAID

## Stato di caricamento {#section_5F55C0101CD44A65BCFE1D124CBDF239}

TVSDK invia i seguenti eventi:

* `AdLoading`
* `AdLoaded`
* `AdStarted`
* `AdPlaying`
* `AdStopped`

Dopo il `AdStopped` TVSDK riprende il contenuto video.

>[!TIP]
>
>Se specifichi un valore pari a zero, TVSDK tenta di caricare l’annuncio fino al suo caricamento o al verificarsi di un errore.

## Ignorare gli annunci {#section_3EA452F420884335AE90DF23C17E416A}

Se il caricamento dell’annuncio richiede troppo tempo o si verificano errori nell’annuncio, TVSDK può ignorarlo e l’annuncio successivo nel pod dell’annuncio viene riprodotto automaticamente.

Se il `AuditudeSettings.customAdLoadTimeout` specifica un numero di secondi maggiore di zero. TVSDK tenta di caricare l’annuncio per la durata specificata. Se non può caricare l’annuncio, l’annuncio viene saltato. Ad esempio, se configuri `AuditudeSettings.customAdLoadTimeout:5`, TVSDK tenta di caricare l’annuncio per un massimo di 5 secondi. Se l’annuncio non viene ancora caricato, viene ignorato.
