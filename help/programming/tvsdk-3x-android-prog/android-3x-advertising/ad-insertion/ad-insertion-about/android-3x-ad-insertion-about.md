---
description: L'inserimento di annunci risolve gli annunci per video-on-demand (VOD), per lo streaming live e per lo streaming lineare con il tracciamento e la riproduzione di annunci. TVSDK effettua le richieste necessarie al server di annunci, riceve informazioni sugli annunci per il contenuto specificato e inserisce gli annunci nel contenuto in più fasi.
seo-description: L'inserimento di annunci risolve gli annunci per video-on-demand (VOD), per lo streaming live e per lo streaming lineare con il tracciamento e la riproduzione di annunci. TVSDK effettua le richieste necessarie al server di annunci, riceve informazioni sugli annunci per il contenuto specificato e inserisce gli annunci nel contenuto in più fasi.
seo-title: Inserire annunci
title: Inserire annunci
uuid: f6636bfa-c96d-4d9d-987a-60292397525a
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Panoramica {#insert-ads-overview}

L&#39;inserimento di annunci risolve gli annunci per video-on-demand (VOD), per lo streaming live e per lo streaming lineare con il tracciamento e la riproduzione di annunci. TVSDK effettua le richieste necessarie al server di annunci, riceve informazioni sugli annunci per il contenuto specificato e inserisce gli annunci nel contenuto in più fasi.

Un messaggio *`ad break`* contiene uno o più annunci che vengono riprodotti in sequenza. TVSDK inserisce gli annunci nel contenuto principale come membri di una o più interruzioni pubblicitarie.

>[!NOTE]
>
>Se l’annuncio contiene errori, TVSDK ignora l’annuncio.