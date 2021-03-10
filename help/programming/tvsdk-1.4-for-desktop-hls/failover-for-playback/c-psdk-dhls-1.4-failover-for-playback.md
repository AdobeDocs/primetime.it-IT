---
description: Lo streaming via Internet richiede una connessione costante e stabile per riprodurre un flusso da un server remoto. Tuttavia, la variabilità della connessione Internet o della riproduzione in streaming di un visualizzatore impedisce la riproduzione a distanza di contenuti multimediali riprodotti localmente.
title: Riproduzione e failover
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 0%

---


# Panoramica {#playback-and-failover-overview}

Lo streaming via Internet richiede una connessione costante e stabile per riprodurre un flusso da un server remoto. Tuttavia, la variabilità della connessione Internet o della riproduzione in streaming di un visualizzatore impedisce la riproduzione a distanza di contenuti multimediali riprodotti localmente.

Primetime non è in grado di proteggere da guasti come un&#39;interruzione dell&#39;ISP o una disconnessione del cavo. Tuttavia, lo streaming Primetime fornisce una protezione di failover per proteggere la riproduzione da alcuni guasti o guasti operativi del server remoto, offrendo ai visualizzatori un&#39;esperienza migliore. TVSDK implementa la protezione del failover per ridurre al minimo le interruzioni di riproduzione e ottenere una riproduzione senza soluzione di continuità nonostante i problemi di trasmissione. Il lettore video passa automaticamente a un set di file multimediali di backup quando non sono disponibili interi rendering o frammenti.
