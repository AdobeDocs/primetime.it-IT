---
description: Per gli annunci (o creativi) Digital Video Ad Serving Template (VAST) che hanno la regola di fallback abilitata, TVSDK tratta un annuncio con un tipo di contenuto multimediale non valido come un annuncio vuoto e tenta di utilizzare gli annunci di fallback al suo posto. Puoi configurare alcuni aspetti del comportamento di fallback.
keywords: annuncio di lunghezza zero;annuncio vuoto
title: Fallback degli annunci per annunci VAST e VMAP
exl-id: 5cabb5f6-b895-48bc-9c9e-b22dd47539bd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---

# Fallback degli annunci per annunci VAST e VMAP {#ad-fallback-for-vast-and-vmap-ads}

Per gli annunci (o creativi) Digital Video Ad Serving Template (VAST) che hanno la regola di fallback abilitata, TVSDK tratta un annuncio con un tipo di contenuto multimediale non valido come un annuncio vuoto e tenta di utilizzare gli annunci di fallback al suo posto. Puoi configurare alcuni aspetti del comportamento di fallback.

La specifica VAST/Digital Video Multiple Ad Playlist (VMAP) stabilisce che per gli annunci che hanno VAST fallback abilitato, gli annunci vuoti attivano automaticamente l’uso degli annunci di fallback. Quando un annuncio VAST è vuoto, TVSDK cerca una sostituzione valida del tipo di file multimediale HLS tra gli annunci di fallback. Quando un annuncio VAST in un wrapper ha un tipo di file multimediale non valido, TVSDK lo considera vuoto. Puoi configurare se TVSDK debba fare lo stesso per gli annunci in linea in una VMAP. Per ulteriori informazioni su VAST `fallbackOnNoAd` funzione, vedi [Modello di server di annunci video digitali (VAST) 3.0](https://www.iab.net/guidelines/508676/digitalvideo/vsuite/vast).

>[!NOTE]
>
>**Annunci a lunghezza zero** - Quando TVSDK rileva una risposta VAST che contiene un annuncio di durata zero o un’interruzione pubblicitaria senza annunci, genera gli eventi AD_BREAK_START/AD_BREAK_COMPLETE per tali interruzioni pubblicitarie di lunghezza zero. *Questo comportamento si applica solo ai flussi VOD.* TVSDK genera questi eventi anche quando l’app utilizza i criteri di salto annuncio.
>
>TVSDK sì *non* attivare gli eventi AD_BREAK_START / AD_BREAK_COMPLETE per i flussi Live, o quando un utente utilizza la funzione di trickplay o cerca di andare oltre l’annuncio di lunghezza zero.
