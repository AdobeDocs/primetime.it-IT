---
description: Per gli annunci (o creativi) Digital Video Ad Serving Template (VAST) con la regola di fallback abilitata, TVSDK tratta un annuncio con un tipo di supporto non valido come un annuncio vuoto e tenta di utilizzare gli annunci di fallback al suo posto. Potete configurare alcuni aspetti del comportamento di fallback.
keywords: zero length ad;empty ad
seo-description: Per gli annunci (o creativi) Digital Video Ad Serving Template (VAST) con la regola di fallback abilitata, TVSDK tratta un annuncio con un tipo di supporto non valido come un annuncio vuoto e tenta di utilizzare gli annunci di fallback al suo posto. Potete configurare alcuni aspetti del comportamento di fallback.
seo-title: Abbandono annunci pubblicitari per annunci VAST e VMAP
title: Abbandono annunci pubblicitari per annunci VAST e VMAP
uuid: 688f0b67-9f5b-4c21-ab33-86d21580fbe9
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Abbandono annunci pubblicitari per annunci VAST e VMAP {#ad-fallback-for-vast-and-vmap-ads}

Per gli annunci (o creativi) Digital Video Ad Serving Template (VAST) con la regola di fallback abilitata, TVSDK tratta un annuncio con un tipo di supporto non valido come un annuncio vuoto e tenta di utilizzare gli annunci di fallback al suo posto. Potete configurare alcuni aspetti del comportamento di fallback.

La specifica VAST/Digital Video Multiple Ad Playlist (VMAP) afferma che per gli annunci che hanno attivato VAST fallback, gli annunci vuoti attivano automaticamente l&#39;uso di fallback pubblicitari. Quando un annuncio VAST è vuoto, TVSDK cerca un tipo di supporto HLS valido sostitutivo tra gli annunci di fallback. Quando un annuncio VAST in un wrapper ha un tipo di supporto non valido, TVSDK tratta l’annuncio come vuoto. Puoi configurare se TVSDK debba fare lo stesso per gli annunci in linea in un VMAP. Per ulteriori informazioni sulla `fallbackOnNoAd` funzione VAST, vedi [Digital Video Ad Serving Template (VAST) 3.0](https://www.iab.net/guidelines/508676/digitalvideo/vsuite/vast).

>[!NOTE]
>
>**Annunci** di lunghezza zero - Quando TVSDK rileva una risposta VAST che contiene un annuncio di durata pari a zero, o un&#39;interruzione annuncio senza annunci, viene attivato gli eventi AD_BREAK_START / AD_BREAK_COMPLETE per quelle interruzioni pubblicitarie di lunghezza zero. *Questo comportamento si applica solo ai flussi VOD.* TVSDK attiva questi eventi anche quando l&#39;app utilizza i criteri degli annunci SKIP.
>
>TVSDK *non* attiva eventi AD_BREAK_START / AD_BREAK_COMPLETE per i flussi in diretta, oppure quando un utente utilizza trickplay o cerca di andare oltre l&#39;annuncio a lunghezza zero.