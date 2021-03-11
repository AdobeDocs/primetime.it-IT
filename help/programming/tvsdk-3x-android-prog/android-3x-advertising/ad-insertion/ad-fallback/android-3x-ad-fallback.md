---
description: Per gli annunci (o creativi) VAST (Digital Video Ad Serving Template) con la regola di fallback abilitata, TVSDK tratta un annuncio con un tipo di supporto non valido come un annuncio vuoto e tenta di utilizzare al suo posto gli annunci di fallback. Puoi configurare alcuni aspetti del comportamento di fallback.
keywords: annuncio a lunghezza zero;annuncio vuoto
title: Fallback dell'annuncio per annunci VAST e VMAP
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---


# Fallback dell&#39;annuncio per annunci VAST e VMAP {#ad-fallback-for-vast-and-vmap-ads}

Per gli annunci (o creativi) VAST (Digital Video Ad Serving Template) con la regola di fallback abilitata, TVSDK tratta un annuncio con un tipo di supporto non valido come un annuncio vuoto e tenta di utilizzare al suo posto gli annunci di fallback. Puoi configurare alcuni aspetti del comportamento di fallback.

La specifica VAST/Digital Video Multiple Ad Playlist (VMAP) afferma che per gli annunci che hanno abilitato il fallback VAST, gli annunci vuoti attivano automaticamente l’uso degli annunci di fallback. Quando un annuncio VAST è vuoto, TVSDK cerca una sostituzione valida del tipo di supporto HLS tra gli annunci di fallback. Quando un annuncio VAST in un wrapper ha un tipo di file multimediale non valido, TVSDK considera questo annuncio come vuoto. Puoi configurare se TVSDK debba fare lo stesso per gli annunci in linea in un VMAP. Per ulteriori informazioni sulla funzione VAST `fallbackOnNoAd`, consulta [Modello di Digital Video Ad Serving (VAST) 3.0](https://www.iab.net/guidelines/508676/digitalvideo/vsuite/vast).

>[!NOTE]
>
>**Annunci a lunghezza zero** : quando TVSDK rileva una risposta VAST che contiene un annuncio di durata pari a zero o un&#39;interruzione pubblicitaria senza annunci, attiva gli eventi AD_BREAK_START / AD_BREAK_COMPLETE per quelle interruzioni pubblicitarie a lunghezza zero. *Questo comportamento si applica solo ai flussi VOD.* TVSDK attiva questi eventi anche quando l’app utilizza i criteri degli annunci SKIP.
>
>TVSDK fa *no* attivare eventi AD_BREAK_START / AD_BREAK_COMPLETE per i flussi live, o quando un utente utilizza trickplay o cerca di andare oltre l&#39;annuncio a lunghezza zero.