---
description: L’inserimento di annunci risolve gli annunci per video on-demand (VOD), per lo streaming live e per lo streaming lineare con tracciamento degli annunci e riproduzione degli annunci. TVSDK effettua le richieste richieste richieste al server di annunci, riceve informazioni sugli annunci per il contenuto specificato e inserisce gli annunci nel contenuto in fasi.
title: Inserisci annunci
exl-id: 899d28b5-92aa-42cb-b7e8-9168fb68dbbd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 0%

---

# Panoramica {#insert-ads-overview}

L’inserimento di annunci risolve gli annunci per video on-demand (VOD), per lo streaming live e per lo streaming lineare con tracciamento degli annunci e riproduzione degli annunci. TVSDK effettua le richieste richieste richieste al server di annunci, riceve informazioni sugli annunci per il contenuto specificato e inserisce gli annunci nel contenuto in fasi.

Un *`ad break`* contiene uno o più annunci riprodotti in sequenza. TVSDK inserisce gli annunci nel contenuto principale come membri di una o più interruzioni pubblicitarie.

>[!NOTE]
>
>Se l’annuncio presenta errori, TVSDK lo ignora.
