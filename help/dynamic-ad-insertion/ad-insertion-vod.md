---
title: Usa  Ad Insertion per VOD
description: Utilizzo di  Ad Insertion per VOD
translation-type: tm+mt
source-git-commit: 7d74e526dbc4c9f623d1ec30e4bc70d9318a89f9
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---


# Usare  Ad Insertion per VOD {#ad-insertion-vod}

Primetime  Ad Insertion supporta l&#39;inserimento di annunci in più risorse VOD, utilizzando i formati standard VAST 3.0+ o VMAP 1.0+.

* [IAB VMAP](https://www.iab.com/wp-content/uploads/2015/06/VMAPv1_0.pdf)

* [IAB VAST](https://www.iab.com/wp-content/uploads/2015/06/VASTv3_0.pdf)

## VOD (Annunci con mappatura server) {#server-mapped-ads}

Primetime  Ad Insertion supporta l&#39;inserimento VOD con annunci inseriti prima dell&#39;inizio della riproduzione utilizzando informazioni sulle timeline degli annunci definite in un formato VMAP.  Il tracciamento annunci specifico per VMAP, ad esempio i beacon breakStart/breakEnd, verrà distribuito con [Ad Tracking](set-up-ad-tracking.md).

## Riproduzione eventi completa (VOD con  Ad Decisioning Cue) {#full-event-replay}

Primetime  Ad Insertion supporta anche risorse VOD specializzate che contengono segnali nel flusso di contenuti stesso, come ad esempio la riproduzione di eventi live registrati in precedenza. Per ulteriori informazioni sui tipi di segnali di decisione degli annunci (o di formati di cue point) supportati, vedere [Utilizzo  Ad Insertion in Live/Linear](ad-insertion-live-linear-stream.md).

Supportiamo sia scenari di richiesta di annunci singoli che scenari di richieste di annunci paralleli per risorse VOD contenenti più di un’interruzione di annuncio. Per ulteriori informazioni, vedere il parametro `ptmulticall` in [Descrizione parametro](/help/dynamic-ad-insertion/msapi-topics/ms-getting-started/ms-api-query-params.md). Sia i formati VAST che VMAP sono supportati per segnali in streaming.
