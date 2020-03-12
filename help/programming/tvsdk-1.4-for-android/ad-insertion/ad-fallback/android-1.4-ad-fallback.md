---
description: Per gli annunci (o creativi) Digital Video Ad Serving Template (VAST) con la regola di fallback abilitata, TVSDK tratta un annuncio con un tipo di supporto non valido come un annuncio vuoto e tenta di utilizzare gli annunci di fallback al suo posto. Potete configurare alcuni aspetti del comportamento di fallback.
seo-description: Per gli annunci (o creativi) Digital Video Ad Serving Template (VAST) con la regola di fallback abilitata, TVSDK tratta un annuncio con un tipo di supporto non valido come un annuncio vuoto e tenta di utilizzare gli annunci di fallback al suo posto. Potete configurare alcuni aspetti del comportamento di fallback.
seo-title: Abbandono annunci pubblicitari per annunci VAST e VMAP
title: Abbandono annunci pubblicitari per annunci VAST e VMAP
uuid: 5469cd22-7121-49f0-8833-2a525c7ef7d0
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Abbandono annunci pubblicitari per annunci VAST e VMAP {#ad-fallback-for-vast-and-vmap-ads}

Per gli annunci (o creativi) Digital Video Ad Serving Template (VAST) con la regola di fallback abilitata, TVSDK tratta un annuncio con un tipo di supporto non valido come un annuncio vuoto e tenta di utilizzare gli annunci di fallback al suo posto. Potete configurare alcuni aspetti del comportamento di fallback.

La specifica VAST/Digital Video Multiple Ad Playlist (VMAP) afferma che per gli annunci in cui è abilitato il fallback VAST, gli annunci vuoti attivano automaticamente l&#39;uso degli fallback pubblicitari. Quando un annuncio VAST è vuoto, TVSDK cerca un tipo di supporto HLS valido sostitutivo tra gli annunci di fallback. Quando un annuncio VAST in un wrapper ha un tipo di supporto non valido, TVSDK tratta l’annuncio come vuoto. Puoi configurare se TVSDK debba fare lo stesso per gli annunci in linea in un VMAP. Per ulteriori informazioni sulla `fallbackOnNoAd` funzione VAST, vedi [Digital Video Ad Serving Template (VAST) 3.0](https://www.iab.net/guidelines/508676/digitalvideo/vsuite/vast).

## Definizione del comportamento fallback ad annunci in linea VMAP {#define-fallback-ad-behavior-for-vmap-inline-ads}

È possibile attivare il fallback quando un elemento multimediale VMAP in linea contiene un tipo di supporto non valido.

1. Impostato `setFallbackOnInvalidCreativeEnabled` per `true` avere VMAP fall back quando il tipo di supporto per un annuncio lineare/inline non è valido per HLS.

   Il valore predefinito è false. Se un annuncio lineare ha un tipo di supporto non valido o non può essere reinserito in un pacchetto, questo flag consente a Primetime ad aveva lo stesso comportamento di fallback come se l&#39;annuncio fosse un wrapper VAST vuoto.

   ```java
   AuditudeSettings result = new AuditudeSettings(); 
   result.setFallbackOnInvalidCreative(true);
   ```

## Comportamento di fallback annunci per VAST e VMAP {#ad-fallback-behavior-for-vast-and-vmap}

Quando Primetime ad Ad Decision rileva un annuncio VAST (creativo) vuoto o con un tipo di supporto non valido per HLS, valuta i fallback pubblicitari per determinare cosa restituire.

<!--<a id="section_9F60AF00CE9645848EAAF8C06A9E426B"></a>-->

In TVSDK, l&#39;unico tipo di supporto valido è `application/x-mpegURL` (M3U8).

In presenza di annunci di fallback indipendenti, il plug-in Primetime ad Decioning esamina questi annunci nell&#39;ordine seguente e restituisce il primo annuncio con un tipo di supporto valido:

1. Se è abilitata la ricompilazione, la prima occorrenza di un annuncio con un tipo di supporto non valido viene trattata come altri tipi di supporti non validi.

   Se la ricompilazione non riesce, questo processo si applica alle occorrenze aggiuntive dell&#39;annuncio.
1. Se TVSDK non trova annunci di fallback validi, restituisce l&#39;annuncio originale con il tipo di supporto non valido.
1. Se viene restituito un annuncio di fallback con un tipo MIME valido al posto dell&#39;annuncio pubblicitario originale, Primetime e Decision invia il codice di errore 403 all&#39;URL dell&#39;errore VAST, se disponibile.
1. Se un annuncio di fallback è un wrapper e restituisce più annunci, vengono restituiti solo gli annunci con il tipo di supporto corretto.

>[!IMPORTANT]
>
>Questo comportamento è sempre abilitato per gli annunci nei wrapper VAST. Per gli annunci VAST in linea in un VMAP, il comportamento è disabilitato per impostazione predefinita, ma l&#39;applicazione può attivarlo.