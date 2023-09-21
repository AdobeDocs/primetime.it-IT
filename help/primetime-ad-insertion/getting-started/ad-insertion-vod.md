---
title: Usa Ad Insertion per VOD
description: Utilizzo di Ad Insertion per VOD
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---

# Usa Ad Insertion per VOD {#ad-insertion-vod}

Primetime Ad Insertion supporta l’inserimento di annunci in più risorse VOD, utilizzando i formati standard VAST 3.0+ o VMAP 1.0+.

* [VMAP IAB](https://www.iab.com/wp-content/uploads/2015/06/VMAPv1_0.pdf)

* [IAB VAST](https://www.iab.com/wp-content/uploads/2015/06/VASTv3_0.pdf)

## VOD (Ad Map) {#server-mapped-ads}

Primetime Ad Insertion supporta l’inserimento VOD con annunci inseriti prima dell’inizio della riproduzione utilizzando le informazioni sulle timeline degli annunci definite in un formato VMAP.  Il tracciamento degli annunci specifico per VMAP, come i beacon breakStart/breakEnd, verrà fornito con [Tracciamento annunci](set-up-ad-tracking.md).

## Riproduzione evento completa (VOD con cue Ad Decisioning) {#full-event-replay}

Primetime Ad Insertion supporta anche risorse VOD specializzate che contengono suggerimenti nel flusso di contenuto stesso, come ad esempio quelli presenti nella riproduzione di eventi live registrati in precedenza. Per ulteriori informazioni sui tipi di suggerimenti per le decisioni sugli annunci (o formati per i cue) supportati, consulta [Utilizzo dell’Ad Insertion in modalità live/lineare](ad-insertion-live-linear-stream.md).

Per le risorse VOD contenenti più di un’interruzione pubblicitaria, sono supportati sia scenari di richiesta singola dell’annuncio che scenari di richiesta multipla parallela. Per ulteriori informazioni, consulta `ptmulticall` parametro in [Descrizione parametro](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md). Per i segnali in streaming sono supportati sia i formati VAST che VMAP.
