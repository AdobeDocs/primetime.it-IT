---
description: Lo streaming su Internet richiede una connessione costante e stabile per riprodurre un flusso da un server remoto. Tuttavia, la variabilità della connessione Internet o della riproduzione in streaming di un visualizzatore impedisce la riproduzione da remoto di contenuti multimediali riprodotti localmente.
seo-description: Lo streaming su Internet richiede una connessione costante e stabile per riprodurre un flusso da un server remoto. Tuttavia, la variabilità della connessione Internet o della riproduzione in streaming di un visualizzatore impedisce la riproduzione da remoto di contenuti multimediali riprodotti localmente.
seo-title: Riproduzione e failover
title: Riproduzione e failover
uuid: 7bbca3fe-88a3-4384-9a63-eb164c956a75
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# Panoramica {#playback-and-failover-overview}

Lo streaming su Internet richiede una connessione costante e stabile per riprodurre un flusso da un server remoto. Tuttavia, la variabilità della connessione Internet o della riproduzione in streaming di un visualizzatore impedisce la riproduzione da remoto di contenuti multimediali riprodotti localmente.

>[!IMPORTANT]
>
>Primetime non è in grado di proteggere da guasti come un&#39;interruzione dell&#39;ISP o una disconnessione del cavo.

Lo streaming Primetime fornisce una protezione del failover per proteggere la riproduzione da alcuni guasti del server remoto o da errori operativi, migliorando l&#39;esperienza di visualizzazione. Nonostante i problemi di trasmissione, TVSDK implementa la protezione contro il failover per ridurre al minimo le interruzioni di riproduzione e ottenere una riproduzione perfetta. Il lettore video passa automaticamente a un set di supporti di backup quando le rappresentazioni o i frammenti interi non sono disponibili.