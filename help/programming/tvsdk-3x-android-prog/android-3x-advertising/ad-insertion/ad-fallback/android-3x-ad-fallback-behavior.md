---
description: Quando Primetime Ad Decision rileva un annuncio VAST (creativo) vuoto o con un tipo di supporto non valido per HLS, valuta i fallback pubblicitari per determinare cosa restituire.
seo-description: Quando Primetime Ad Decision rileva un annuncio VAST (creativo) vuoto o con un tipo di supporto non valido per HLS, valuta i fallback pubblicitari per determinare cosa restituire.
seo-title: Comportamento di fallback annunci per VAST e VMAP
title: Comportamento di fallback annunci per VAST e VMAP
uuid: 612416b9-d070-42e2-b68b-74ba52023345
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
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