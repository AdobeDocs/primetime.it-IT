---
description: Quando Primetime Ad Decision rileva un annuncio VAST (creativo) vuoto o con un tipo di supporto non valido per HLS, valuta i fallback pubblicitari per determinare cosa restituire.
seo-description: Quando Primetime Ad Decision rileva un annuncio VAST (creativo) vuoto o con un tipo di supporto non valido per HLS, valuta i fallback pubblicitari per determinare cosa restituire.
seo-title: Comportamento di fallback annunci per VAST e VMAP
title: Comportamento di fallback annunci per VAST e VMAP
uuid: 50e17372-fd29-4792-aafa-8f9c21cc42c6
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---


# Comportamento di fallback annunci per VAST e VMAP {#ad-fallback-behavior-for-vast-and-vmap}

Quando Primetime Ad Decision rileva un annuncio VAST (creativo) vuoto o con un tipo di supporto non valido per HLS, valuta i fallback pubblicitari per determinare cosa restituire.

<!--<a id="section_9F60AF00CE9645848EAAF8C06A9E426B"></a>-->

In TVSDK, l&#39;unico tipo di supporto valido è `application/x-mpegURL` (M3U8).

In presenza di annunci di fallback indipendenti, il plug-in Primetime ad Decisionioningesamina questi annunci nell&#39;ordine seguente e restituisce il primo annuncio con un tipo di supporto valido:

1. Se è abilitata la ricompilazione, la prima occorrenza di un annuncio con un tipo di supporto non valido viene trattata come altri tipi di supporti non validi.

   Se la ricompilazione non riesce, questo processo si applica alle occorrenze aggiuntive dell&#39;annuncio.
1. Se TVSDK non trova annunci di fallback validi, restituisce l&#39;annuncio originale con il tipo di supporto non valido.
1. Se viene restituito un annuncio di fallback con un tipo MIME valido al posto dell&#39;annuncio pubblicitario originale, Primetime e Decision invia il codice di errore 403 all&#39;URL dell&#39;errore VAST, se disponibile.
1. Se un annuncio di fallback è un wrapper e restituisce più annunci, vengono restituiti solo gli annunci con il tipo di supporto corretto.

>[!IMPORTANT]
>
>Questo comportamento è sempre abilitato per gli annunci nei wrapper VAST. Per gli annunci VAST in linea in un VMAP, il comportamento è disabilitato per impostazione predefinita, ma l&#39;applicazione può attivarlo.

