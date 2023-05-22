---
description: L’inserimento di annunci risolve gli annunci per video on-demand (VOD), per lo streaming live e per lo streaming lineare con tracciamento degli annunci e riproduzione degli annunci. TVSDK effettua le richieste richieste richieste al server di annunci, riceve informazioni sugli annunci per il contenuto specificato e inserisce gli annunci nel contenuto in fasi.
title: Inserimento annunci
exl-id: 390036e2-2459-4cfb-a336-640d816bdaad
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 0%

---

# Panoramica {#insert-ads-overview}

L’inserimento di annunci risolve gli annunci per video on-demand (VOD), per lo streaming live e per lo streaming lineare con tracciamento degli annunci e riproduzione degli annunci. TVSDK effettua le richieste richieste richieste al server di annunci, riceve informazioni sugli annunci per il contenuto specificato e inserisce gli annunci nel contenuto in fasi.

Un’interruzione pubblicitaria contiene uno o più annunci riprodotti in sequenza. TVSDK inserisce gli annunci nel contenuto principale come membri di una o più interruzioni pubblicitarie.

>[!TIP]
>
>Se l’annuncio presenta errori, TVSDK lo ignora.
