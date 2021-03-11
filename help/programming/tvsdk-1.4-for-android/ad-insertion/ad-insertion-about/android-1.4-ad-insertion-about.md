---
description: L'inserimento di annunci risolve gli annunci per video-on-demand (VOD), per streaming live e per streaming lineare con tracciamento degli annunci e riproduzione di annunci. TVSDK invia le richieste richieste al server di annunci, riceve le informazioni sugli annunci per il contenuto specificato e inserisce gli annunci nel contenuto in più fasi.
title: Inserimento di annunci
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 0%

---


# Panoramica {#insert-ads-overview}

L&#39;inserimento di annunci risolve gli annunci per video-on-demand (VOD), per streaming live e per streaming lineare con tracciamento degli annunci e riproduzione di annunci. TVSDK invia le richieste richieste al server di annunci, riceve le informazioni sugli annunci per il contenuto specificato e inserisce gli annunci nel contenuto in più fasi.

Un&#39;interruzione pubblicitaria contiene uno o più annunci che vengono riprodotti in sequenza. TVSDK inserisce gli annunci nel contenuto principale come membri di una o più interruzioni pubblicitarie.

>[!TIP]
>
>Se l’annuncio contiene errori, TVSDK ignora l’annuncio.