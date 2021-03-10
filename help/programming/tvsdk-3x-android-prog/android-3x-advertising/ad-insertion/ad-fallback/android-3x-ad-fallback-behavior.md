---
description: Quando Primetime ad decision rileva un annuncio VAST (creativo) vuoto o con un tipo di file multimediale non valido per HLS, valuta i fallback pubblicitari per determinare cosa restituire.
title: Comportamento di fallback degli annunci per VAST e VMAP
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---


# Comportamento di fallback degli annunci per VAST e VMAP {#ad-fallback-behavior-for-vast-and-vmap}

Quando Primetime ad decision rileva un annuncio VAST (creativo) vuoto o con un tipo di file multimediale non valido per HLS, valuta i fallback pubblicitari per determinare cosa restituire.

<!--<a id="section_9F60AF00CE9645848EAAF8C06A9E426B"></a>-->

In TVSDK, l&#39;unico tipo di supporto valido è `application/x-mpegURL` (M3U8).

In presenza di annunci di fallback autonomi, il plug-in Primetime ad decision esamina questi annunci nell&#39;ordine seguente e restituisce il primo annuncio con un tipo di supporto valido:

1. Se è abilitato il repackaging, la prima occorrenza di un annuncio con un tipo di supporto non valido viene trattata come altri tipi di supporto non validi.

   In caso di errore di repackaging, questo processo si applica alle occorrenze aggiuntive dell&#39;annuncio.
1. Se TVSDK non trova annunci di fallback validi, restituisce l&#39;annuncio originale con il tipo di supporto non valido.
1. Se viene restituito un annuncio di fallback con un tipo MIME valido invece dell’annuncio originale, Primetime ad decision invia il codice di errore 403 all’URL di errore VAST, se disponibile.
1. Se un annuncio di fallback è un wrapper e restituisce più annunci, vengono restituiti solo gli annunci con il tipo di supporto corretto.

>[!IMPORTANT]
>
>Questo comportamento è sempre abilitato per gli annunci nei wrapper VAST. Per gli annunci VAST in linea in un VMAP, il comportamento è disabilitato per impostazione predefinita, ma l&#39;applicazione può abilitarlo.