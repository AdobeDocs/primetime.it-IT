---
description: Per gli annunci (o creativi) VAST (Digital Video Ad Serving Template) con la regola di fallback abilitata, TVSDK tratta un annuncio con un tipo di supporto non valido come un annuncio vuoto e tenta di utilizzare al suo posto gli annunci di fallback. Puoi configurare alcuni aspetti del comportamento di fallback.
title: Fallback dell'annuncio per annunci VAST e VMAP
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---


# Fallback dell&#39;annuncio per annunci VAST e VMAP {#ad-fallback-for-vast-and-vmap-ads}

Per gli annunci (o creativi) VAST (Digital Video Ad Serving Template) con la regola di fallback abilitata, TVSDK tratta un annuncio con un tipo di supporto non valido come un annuncio vuoto e tenta di utilizzare al suo posto gli annunci di fallback. Puoi configurare alcuni aspetti del comportamento di fallback.

La specifica VAST/Digital Video Multiple Ad Playlist (VMAP) indica che per gli annunci in cui è abilitato il fallback VAST, gli annunci vuoti attivano automaticamente l’uso degli annunci di fallback. Quando un annuncio VAST è vuoto, TVSDK cerca una sostituzione valida del tipo di supporto HLS tra gli annunci di fallback. Quando un annuncio VAST in un wrapper ha un tipo di file multimediale non valido, TVSDK considera questo annuncio come vuoto. Puoi configurare se TVSDK debba fare lo stesso per gli annunci in linea in un VMAP. Per ulteriori informazioni sulla funzione VAST `fallbackOnNoAd`, consulta [Modello di Digital Video Ad Serving (VAST) 3.0](https://www.iab.net/guidelines/508676/digitalvideo/vsuite/vast).

## Definire il comportamento di fallback ad per gli annunci in linea VMAP {#section_D90BB3C6E539472EABF000C0F616DBE2}

È possibile attivare il fallback quando un annuncio VMAP in linea contiene un tipo di supporto non valido.

1. Impostare `FallbackOnInvalidCreativeEnabled` su `YES` per far sì che VMAP torni quando il tipo di supporto per un annuncio lineare/in linea non è valido per HLS.

   >[!NOTE]
   >
   >Il valore predefinito è NO. Se un annuncio lineare non riesce perché ha un tipo di supporto non valido o perché non può essere ricompilato, questo flag consente a Primetime ad DECISioning di seguire lo stesso comportamento di fallback come se l&#39;annuncio fosse un wrapper VAST vuoto.

   ```
   PTAuditudeMetadata *adMetadata = [[[PTAuditudeMetadata alloc] init] autorelease]; 
   adMetadata.isFallbackOnInvalidCreativeEnabled = YES;
   ```

## Comportamento di fallback degli annunci per VAST e VMAP {#section_5B6716CC49CC4C40964CFE9F122C57A6}

Quando Primetime ad decision rileva un annuncio VAST (creativo) vuoto o con un tipo di file multimediale non valido per HLS, valuta i fallback pubblicitari per determinare cosa restituire.

In TVSDK, l&#39;unico tipo di supporto valido è `application/x-mpegURL` (M3U8).

In presenza di annunci di fallback autonomi, il plug-in Primetime ad decisioning esamina questi annunci nell&#39;ordine seguente e restituisce il primo annuncio con un tipo di supporto valido:

1. Se è abilitato il repackaging, la prima occorrenza di un annuncio con un tipo di supporto non valido viene trattata come altri tipi di supporto non validi.

   In caso di errore di repackaging, questo processo si applica alle occorrenze aggiuntive dell&#39;annuncio.
1. Se TVSDK non trova annunci di fallback validi, restituisce l&#39;annuncio originale con il tipo di supporto non valido.
1. Se viene restituito un annuncio di fallback con un tipo MIME valido invece dell’annuncio originale, Primetime ad decision invia il codice di errore 403 all’URL di errore VAST, se disponibile.
1. Se un annuncio di fallback è un wrapper e restituisce più annunci, vengono restituiti solo gli annunci con il tipo di supporto corretto.

>[!IMPORTANT]
>
>Questo comportamento è sempre abilitato per gli annunci nei wrapper VAST. Per gli annunci VAST in linea in un VMAP, il comportamento è disabilitato per impostazione predefinita, ma l&#39;applicazione può abilitarlo.