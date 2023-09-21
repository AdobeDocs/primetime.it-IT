---
description: Per gli annunci (o creativi) Digital Video Ad Serving Template (VAST) che hanno la regola di fallback abilitata, TVSDK tratta un annuncio con un tipo di contenuto multimediale non valido come un annuncio vuoto e tenta di utilizzare gli annunci di fallback al suo posto. Puoi configurare alcuni aspetti del comportamento di fallback.
title: Fallback degli annunci per annunci VAST e VMAP
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 0%

---

# Fallback degli annunci per annunci VAST e VMAP {#ad-fallback-for-vast-and-vmap-ads}

Per gli annunci (o creativi) Digital Video Ad Serving Template (VAST) che hanno la regola di fallback abilitata, TVSDK tratta un annuncio con un tipo di contenuto multimediale non valido come un annuncio vuoto e tenta di utilizzare gli annunci di fallback al suo posto. Puoi configurare alcuni aspetti del comportamento di fallback.

La specifica VAST/Digital Video Multiple Ad Playlist (VMAP) stabilisce che per gli annunci in cui è abilitato il fallback VAST, gli annunci vuoti attivano automaticamente l’uso degli annunci di fallback. Quando un annuncio VAST è vuoto, TVSDK cerca una sostituzione valida del tipo di file multimediale HLS tra gli annunci di fallback. Quando un annuncio VAST in un wrapper ha un tipo di file multimediale non valido, TVSDK lo considera vuoto. Puoi configurare se TVSDK debba fare lo stesso per gli annunci in linea in una VMAP. Per ulteriori informazioni su VAST `fallbackOnNoAd` funzione, vedi [Modello di server di annunci video digitali (VAST) 3.0](https://www.iab.net/guidelines/508676/digitalvideo/vsuite/vast).

## Definire il comportamento degli annunci di fallback per gli annunci in linea VMAP {#define-fallback-ad-behavior-for-vmap-inline-ads}

È possibile attivare il fallback quando un annuncio VMAP in linea contiene un tipo di supporto non valido.

1. Imposta `fallbackOnInvalidCreative` su true per eseguire il fallback di VMAP quando il tipo di supporto per un annuncio lineare/in linea non è valido per HLS.

   Il valore predefinito è false. Se un annuncio lineare ha esito negativo perché presenta un tipo di contenuto multimediale non valido o perché l’annuncio non può essere ricompilato, questo flag consente a Primetime ad decisioning di seguire lo stesso comportamento di fallback come se l’annuncio fosse un wrapper VAST vuoto.

   ```
   var auditudeMetadata:AuditudeSettings = new AuditudeSettings(); 
   auditudeMetadata.fallbackOnInvalidCreative = true;
   ```

## Comportamento di fallback degli annunci per VAST e VMAP {#ad-fallback-behavior-for-vast-and-vmap}

Quando Primetime ad decisioning rileva un annuncio VAST (creativo) vuoto o con un tipo di file multimediale non valido per HLS, valuta gli annunci di fallback per determinare cosa restituire.

<!--<a id="section_9F60AF00CE9645848EAAF8C06A9E426B"></a>-->

In TVSDK, gli unici tipi di file multimediali validi sono `application/x-shockwave-flash` (VPAID) `application/x-mpegURL` (m3u8)

In presenza di annunci di fallback autonomi, il plug-in Primetime ad decisioning esamina tali annunci nell’ordine seguente e restituisce il primo annuncio con un tipo di file multimediale valido:

1. Se è abilitata la ricompilazione, la prima occorrenza di un annuncio con un tipo di file multimediale non valido viene trattata come altri tipi di file multimediali non validi.

   Se il riconfezionamento non riesce, questo processo si applica alle occorrenze aggiuntive dell’annuncio.
1. Se TVSDK non trova annunci di fallback validi, restituisce l’annuncio originale con il tipo di file multimediale non valido.
1. Se invece dell’annuncio originale viene restituito un annuncio di fallback con un tipo MIME valido, Primetime ad decisioning invia il codice di errore 403 all’URL dell’errore VAST, se disponibile.
1. Se un annuncio di fallback è un wrapper e restituisce più annunci, vengono restituiti solo gli annunci con il tipo di file multimediale corretto.

>[!IMPORTANT]
>
>Questo comportamento è sempre abilitato per gli annunci nei wrapper VAST. Per gli annunci VAST in linea in una VMAP, il comportamento è disabilitato per impostazione predefinita, ma l’applicazione può abilitarlo.
