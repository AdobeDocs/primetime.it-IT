---
title: Memorizzazione in cache
description: Memorizzazione in cache
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---

# Memorizzazione in cache HTTP {#caching}

Per impostazione predefinita, Primetime Ad Insertion rispetta le intestazioni di controllo della cache HTTP durante il recupero delle creatività degli annunci e del contenuto.  Questo può ridurre drasticamente la quantità di richieste di rete che gli Ad Insertion di Primetime devono effettuare alla rete CDN in tutti i client.  Per il caching, l’Adobe consiglia le seguenti impostazioni e prevede l’invio dell’intestazione HTTP `max-age` dalla rete CDN.  Contatta il rappresentante CDN per abilitare queste intestazioni nei flussi video e pubblicitari.

## Per contenuti live/lineari {#caching-live-linear-content}

* Manifesto principale: 24 ore, oppure Cache-Control: max-age=86400
* Manifesto multimediale: 1 secondo, oppure Cache-Control: max-age=1

## Per contenuti VOD {#caching-vod-content}

* Manifesto principale: 24 ore, oppure Cache-Control: max-age=86400
* Manifesto multimediale: 24 ore, oppure Cache-Control: max-age=86400
