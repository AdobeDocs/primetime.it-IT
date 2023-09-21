---
title: Ottimizzare i tempi di avvio dei video
description: Ottimizzazione dei tempi di avvio dei video
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---

# Panoramica sull’ottimizzazione dei tempi di avvio dei video {#optimize-video-start-up-times}

Primetime Ad Insertion fornisce diverse funzioni per ottimizzare il tempo di avvio del video, ad esempio il caching e le regole per l’ottimizzazione di route/protocollo. Di seguito sono riportati alcuni altri consigli per garantire tempi di avvio video più rapidi quando si utilizza Primetime Ad Insertion:

* Distribuisci tutti gli annunci e i contenuti dalle reti CDN (Content Delivery Networks)

* Riduci o rimuovi gli handshake TLS tra l’Ad Insertion Primetime e i CDN. Per ulteriori informazioni, consulta [Ottimizzare route e protocolli](optimize-routes-protocols.md).

* Distribuisci frammenti di annunci e contenuti dalla stessa rete CDN

* Inserisci intestazioni di controllo cache per contenuti e manifesti VOD/live

* Ridurre o rimuovere i provider di annunci o i creativi di annunci che sono lenti a rispondere
