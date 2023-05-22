---
description: Per gli annunci (o creativi) Digital Video Ad Serving Template (VAST) che hanno la regola di fallback abilitata, TVSDK tratta un annuncio con un tipo di contenuto multimediale non valido come un annuncio vuoto e tenta di utilizzare gli annunci di fallback al suo posto. Puoi configurare alcuni aspetti del comportamento di fallback.
title: Fallback degli annunci per annunci VAST e VMAP
exl-id: 5c469686-f8db-463a-ad1a-cb64e9192fb7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---

# Fallback degli annunci per annunci VAST e VMAP {#ad-fallback-for-vast-and-vmap-ads}

Per gli annunci (o creativi) Digital Video Ad Serving Template (VAST) che hanno la regola di fallback abilitata, TVSDK tratta un annuncio con un tipo di contenuto multimediale non valido come un annuncio vuoto e tenta di utilizzare gli annunci di fallback al suo posto. Puoi configurare alcuni aspetti del comportamento di fallback.

La specifica VAST/Digital Video Multiple Ad Playlist (VMAP) stabilisce che per gli annunci in cui è abilitato il fallback VAST, gli annunci vuoti attivano automaticamente l’uso degli annunci di fallback. Quando un annuncio VAST è vuoto, TVSDK cerca una sostituzione valida del tipo di file multimediale HLS tra gli annunci di fallback. Quando un annuncio VAST in un wrapper ha un tipo di file multimediale non valido, TVSDK lo considera vuoto. Puoi configurare se TVSDK debba fare lo stesso per gli annunci in linea in una VMAP. Per ulteriori informazioni su VAST `fallbackOnNoAd` funzione, vedi [Modello di server di annunci video digitali (VAST) 3.0](https://www.iab.net/guidelines/508676/digitalvideo/vsuite/vast).

## Definire il comportamento degli annunci di fallback per gli annunci in linea VMAP {#section_D90BB3C6E539472EABF000C0F616DBE2}

È possibile attivare il fallback quando un annuncio VMAP in linea contiene un tipo di supporto non valido.

1. Imposta `FallbackOnInvalidCreativeEnabled` a `YES` per eseguire il fallback di VMAP quando il tipo di supporto per un annuncio lineare/in linea non è valido per HLS.

   >[!NOTE]
   >
   >Il valore predefinito è NO. Se un annuncio lineare ha esito negativo perché presenta un tipo di contenuto multimediale non valido o perché l’annuncio non può essere ricompilato, questo flag consente a Primetime ad decisioning di seguire lo stesso comportamento di fallback come se l’annuncio fosse un wrapper VAST vuoto.

   ```
   PTAuditudeMetadata *adMetadata = [[[PTAuditudeMetadata alloc] init] autorelease]; 
   adMetadata.isFallbackOnInvalidCreativeEnabled = YES;
   ```

## Comportamento di fallback degli annunci per VAST e VMAP {#section_5B6716CC49CC4C40964CFE9F122C57A6}

Quando Primetime ad decisioning rileva un annuncio VAST (creativo) vuoto o con un tipo di file multimediale non valido per HLS, valuta gli annunci di fallback per determinare cosa restituire.

In TVSDK, l’unico tipo di file multimediale valido è `application/x-mpegURL` (M3U8).

In presenza di annunci di fallback autonomi, il plug-in Primetime ad decisioning esamina tali annunci nell’ordine seguente e restituisce il primo annuncio con un tipo di file multimediale valido:

1. Se è abilitata la ricompilazione, la prima occorrenza di un annuncio con un tipo di file multimediale non valido viene trattata come altri tipi di file multimediali non validi.

   Se il riconfezionamento non riesce, questo processo si applica alle occorrenze aggiuntive dell’annuncio.
1. Se TVSDK non trova annunci di fallback validi, restituisce l’annuncio originale con il tipo di file multimediale non valido.
1. Se invece dell’annuncio originale viene restituito un annuncio di fallback con un tipo MIME valido, Primetime ad decisioning invia il codice di errore 403 all’URL dell’errore VAST, se disponibile.
1. Se un annuncio di fallback è un wrapper e restituisce più annunci, vengono restituiti solo gli annunci con il tipo di file multimediale corretto.

>[!IMPORTANT]
>
>Questo comportamento è sempre abilitato per gli annunci nei wrapper VAST. Per gli annunci VAST in linea in una VMAP, il comportamento è disabilitato per impostazione predefinita, ma l’applicazione può abilitarlo.
