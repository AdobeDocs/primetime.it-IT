---
title: Caching
description: null
translation-type: tm+mt
source-git-commit: 76dc54fabdae400ad708ba83fcf6f7fd5caa2b22
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---


# Cache HTTP {#caching}

Primetime  Ad Insertion per impostazione predefinita rispetta le intestazioni di controllo della cache HTTP al momento del recupero di contenuti e creativi per gli annunci.  Questo può ridurre drasticamente la quantità di richieste di rete necessarie per il Ad Insertion Primetime  per effettuare il collegamento alla rete CDN tra tutti i client.  Per il caching,  Adobe consiglia le seguenti impostazioni e prevede l&#39;invio dell&#39;intestazione HTTP `max-age` dalla rete CDN.  Contattate il rappresentante CDN per abilitare queste intestazioni sui flussi video e sui flussi di annunci.

## Per contenuti live/lineari {#caching-live-linear-content}

* manifest principale: 24 ore o controllo cache: max-age=86400
* manifest multimediale: 1 secondo, o controllo cache: max-age=1

## Per contenuti VOD {#caching-vod-content}

* manifest principale: 24 ore o controllo cache: max-age=86400
* manifest multimediale: 24 ore o controllo cache: max-age=86400
