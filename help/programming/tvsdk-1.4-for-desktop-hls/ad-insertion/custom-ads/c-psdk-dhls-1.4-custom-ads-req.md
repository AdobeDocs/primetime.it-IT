---
description: Video Player Ad-Serving Interface Definition (VPAID) fornisce un'interfaccia comune per riprodurre annunci video. VPAID offre agli utenti un’esperienza multimediale avanzata e consente agli editori di eseguire meglio il targeting degli annunci, tenere traccia delle impressioni degli annunci e monetizzare i contenuti video.
title: Requisiti degli annunci personalizzati
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---


# Requisiti degli annunci personalizzati {#custom-ad-requirements}

Il lettore TVSDK può riprodurre annunci VPAID (Digital Video Player Ad-Interface Definition) e visualizzare lo stato di caricamento dell&#39;annuncio. Se ci sono errori nell’annuncio, o se il caricamento degli annunci richiede troppo tempo, TVSDK ignora questi annunci.

Video Player Ad-Serving Interface Definition (VPAID) fornisce un&#39;interfaccia comune per riprodurre annunci video. VPAID offre agli utenti un’esperienza multimediale avanzata e consente agli editori di eseguire meglio il targeting degli annunci, tenere traccia delle impressioni degli annunci e monetizzare i contenuti video.

<!--<a id="section_9A358902CBC24999BA34206EE2029616"></a>-->

Il TVSDK supporta le seguenti funzioni:

* Versione 1.0 e 2.0 della specifica VPAID
* Annunci VPAID lineari su contenuti video on demand (VOD)
* Annunci VPAID Flash

   Gli annunci VPAID devono essere basati su Flash e la risposta dell’annuncio deve identificare il tipo di supporto dell’annuncio VPAID come `application/x-shockwave-flash`.

Le seguenti funzionalità non sono supportate:

* Annunci non lineari come annunci di sovrapposizione e annunci dinamici di accompagnamento
* Precaricamento degli annunci VPAID
* Annunci VPAID nel contenuto live
* Annunci VPAID JavaScript

## Caricamento dello stato {#section_5F55C0101CD44A65BCFE1D124CBDF239}

Il TVSDK invia i seguenti eventi:

* `AdLoading`
* `AdLoaded`
* `AdStarted`
* `AdPlaying`
* `AdStopped`

Dopo l’evento `AdStopped` , il TVSDK riprende il contenuto video.

>[!TIP]
>
>Se specifichi un valore pari a zero, TVSDK tenta di caricare l’annuncio finché non viene caricato o si è verificato un errore.

## Annunci ignoranti {#section_3EA452F420884335AE90DF23C17E416A}

Se il caricamento dell’annuncio richiede troppo tempo o si verificano errori nell’annuncio, il TVSDK può ignorare l’annuncio e l’annuncio successivo nel contenitore dell’annuncio viene riprodotto automaticamente.

Se l’impostazione `AuditudeSettings.customAdLoadTimeout` specifica un numero di secondi maggiore di zero, TVSDK tenta di caricare l’annuncio nella durata specificata. Se non è in grado di caricare l’annuncio, l’annuncio viene ignorato. Ad esempio, se configuri `AuditudeSettings.customAdLoadTimeout:5`, TVSDK tenta di caricare l’annuncio per un massimo di 5 secondi. Se l’annuncio non viene ancora caricato, viene ignorato.
