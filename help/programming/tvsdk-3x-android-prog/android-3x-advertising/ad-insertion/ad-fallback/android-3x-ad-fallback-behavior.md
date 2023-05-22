---
description: Quando Primetime ad decisioningrileva un annuncio VAST (creativo) vuoto o con un tipo di file multimediale non valido per HLS, valuta gli annunci di fallback per determinare cosa restituire.
title: Comportamento di fallback degli annunci per VAST e VMAP
exl-id: 65814b91-6528-4eea-abfb-f45dd2dbb899
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---

# Comportamento di fallback degli annunci per VAST e VMAP {#ad-fallback-behavior-for-vast-and-vmap}

Quando Primetime ad decisioningrileva un annuncio VAST (creativo) vuoto o con un tipo di file multimediale non valido per HLS, valuta gli annunci di fallback per determinare cosa restituire.

<!--<a id="section_9F60AF00CE9645848EAAF8C06A9E426B"></a>-->

In TVSDK, l’unico tipo di file multimediale valido è `application/x-mpegURL` (M3U8).

In presenza di annunci di fallback autonomi, il plug-in Primetime ad decisioningesamina tali annunci nell’ordine seguente e restituisce il primo annuncio con un tipo di file multimediale valido:

1. Se è abilitata la ricompilazione, la prima occorrenza di un annuncio con un tipo di file multimediale non valido viene trattata come altri tipi di file multimediali non validi.

   Se il riconfezionamento non riesce, questo processo si applica alle occorrenze aggiuntive dell’annuncio.
1. Se TVSDK non trova annunci di fallback validi, restituisce l’annuncio originale con il tipo di file multimediale non valido.
1. Se invece dell’annuncio originale viene restituito un annuncio di fallback con un tipo MIME valido, Primetime ad decisioninginvia il codice di errore 403 all’URL dell’errore VAST, se disponibile.
1. Se un annuncio di fallback è un wrapper e restituisce più annunci, vengono restituiti solo gli annunci con il tipo di file multimediale corretto.

>[!IMPORTANT]
>
>Questo comportamento è sempre abilitato per gli annunci nei wrapper VAST. Per gli annunci VAST in linea in una VMAP, il comportamento è disabilitato per impostazione predefinita, ma l’applicazione può abilitarlo.
