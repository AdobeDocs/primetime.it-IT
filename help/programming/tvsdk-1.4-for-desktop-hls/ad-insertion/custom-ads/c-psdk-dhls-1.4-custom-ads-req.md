---
description: Video Player Ad-Serving Interface Definition (VPAID) fornisce un'interfaccia comune per la riproduzione di annunci video. VPAID offre agli utenti un'esperienza multimediale avanzata e consente agli editori di eseguire il targeting degli annunci, tenere traccia delle impressioni degli annunci e monetizzare i contenuti video.
seo-description: Video Player Ad-Serving Interface Definition (VPAID) fornisce un'interfaccia comune per la riproduzione di annunci video. VPAID offre agli utenti un'esperienza multimediale avanzata e consente agli editori di eseguire il targeting degli annunci, tenere traccia delle impressioni degli annunci e monetizzare i contenuti video.
seo-title: Requisiti annunci personalizzati
title: Requisiti annunci personalizzati
uuid: 6d4ba87b-ffe5-467d-8ab5-9795928c2f69
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 0%

---


# Requisiti annunci personalizzati {#custom-ad-requirements}

Il lettore TVSDK può riprodurre annunci VPAID (Digital Video Player Ad-Interface Definition) e visualizzare lo stato di caricamento dell&#39;annuncio. In caso di errori nell’annuncio, o se il caricamento degli annunci richiede troppo tempo, TVSDK ignora questi annunci.

Video Player Ad-Serving Interface Definition (VPAID) fornisce un&#39;interfaccia comune per la riproduzione di annunci video. VPAID offre agli utenti un&#39;esperienza multimediale avanzata e consente agli editori di eseguire il targeting degli annunci, tenere traccia delle impressioni degli annunci e monetizzare i contenuti video.

<!--<a id="section_9A358902CBC24999BA34206EE2029616"></a>-->

TVSDK supporta le seguenti funzionalità:

* Versioni 1.0 e 2.0 della specifica VPAID
* Annunci VPAID lineari su contenuti video su richiesta (VOD)
* Annunci VPAID Flash

   Gli annunci VPAID devono essere basati sul Flash e la risposta dell&#39;annuncio deve identificare il tipo di supporto dell&#39;annuncio VPAID come `application/x-shockwave-flash`.

Le seguenti funzionalità non sono supportate:

* Annunci non lineari come annunci di sovrapposizione e annunci di accompagnamento dinamici
* Precaricamento degli annunci VPAID
* Annunci VPAID nel contenuto live
* Annunci VPAID JavaScript

## Stato di caricamento {#section_5F55C0101CD44A65BCFE1D124CBDF239}

TVSDK invia gli eventi seguenti:

* `AdLoading`
* `AdLoaded`
* `AdStarted`
* `AdPlaying`
* `AdStopped`

Dopo l&#39;evento `AdStopped`, TVSDK riprende il contenuto video.

>[!TIP]
>
>Se specificate un valore pari a zero, TVSDK tenta di caricare l&#39;annuncio fino al suo caricamento o si è verificato un errore.

## Annunci ignoranti {#section_3EA452F420884335AE90DF23C17E416A}

Se il caricamento dell’annuncio richiede troppo tempo o si verificano errori nell’annuncio, TVSDK può ignorare l’annuncio e l’annuncio successivo nel contenitore dell’annuncio viene riprodotto automaticamente.

Se l&#39;impostazione `AuditudeSettings.customAdLoadTimeout` specifica un numero di secondi maggiore di zero, TVSDK tenta di caricare l&#39;annuncio alla durata specificata. Se non è in grado di caricare l’annuncio, l’annuncio viene ignorato. Ad esempio, se configurate `AuditudeSettings.customAdLoadTimeout:5`, TVSDK tenta di caricare l&#39;annuncio per un massimo di 5 secondi. Se l&#39;annuncio non viene ancora caricato, viene ignorato.
