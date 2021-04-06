---
title: Memorizzazione in cache
description: Memorizzazione in cache
copied-description: true
exl-id: c12c2345-db55-468a-b4b5-5a9e1364a46d
translation-type: tm+mt
source-git-commit: 3e63c187f12d1bff53370bbcde4d6a77f58f3b4f
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---

# Memorizzazione in cache HTTP {#caching}

Primetime Ad Insertion per impostazione predefinita rispetta le intestazioni di controllo della cache HTTP durante il recupero di contenuti e creativi di annunci.  Questo può ridurre drasticamente la quantità di richieste di rete necessarie a Primetime Ad Insertion per effettuare l’accesso alla rete CDN in tutti i client.  Per il caching, Adobe consiglia le seguenti impostazioni e richiede l’invio dell’intestazione HTTP `max-age` dalla rete CDN.  Contatta il tuo rappresentante CDN per abilitare queste intestazioni sui flussi video e sui flussi di annunci.

## Per contenuti live/lineari {#caching-live-linear-content}

* Manifesto principale: 24 ore o controllo della cache: max-age=86400
* Manifesto multimediale: 1 secondo, o controllo cache: max-age=1

## Per contenuto VOD {#caching-vod-content}

* Manifesto principale: 24 ore o controllo della cache: max-age=86400
* Manifesto multimediale: 24 ore o controllo della cache: max-age=86400
