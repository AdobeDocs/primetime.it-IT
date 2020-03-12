---
description: Lo streaming su Internet richiede una connessione costante e stabile per riprodurre un flusso da un server remoto. Tuttavia, la variabilità della connessione Internet o della riproduzione in streaming di un visualizzatore impedisce la riproduzione da remoto di contenuti multimediali riprodotti localmente.
seo-description: Lo streaming su Internet richiede una connessione costante e stabile per riprodurre un flusso da un server remoto. Tuttavia, la variabilità della connessione Internet o della riproduzione in streaming di un visualizzatore impedisce la riproduzione da remoto di contenuti multimediali riprodotti localmente.
seo-title: Riproduzione e failover
title: Riproduzione e failover
uuid: 511f16b9-2b86-42c1-8d89-09b26534200b
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Panoramica {#playback-and-failover-overview}

Lo streaming su Internet richiede una connessione costante e stabile per riprodurre un flusso da un server remoto. Tuttavia, la variabilità della connessione Internet o della riproduzione in streaming di un visualizzatore impedisce la riproduzione da remoto di contenuti multimediali riprodotti localmente.

>[!IMPORTANT]
>
>Primetime non è in grado di proteggere da guasti come un&#39;interruzione dell&#39;ISP o una disconnessione del cavo.

Lo streaming Primetime fornisce una protezione del failover per proteggere la riproduzione da alcuni guasti del server remoto o da errori operativi, migliorando l&#39;esperienza di visualizzazione. Nonostante i problemi di trasmissione, TVSDK implementa la protezione contro il failover per ridurre al minimo le interruzioni di riproduzione e ottenere una riproduzione perfetta. Il lettore video passa automaticamente a un set di supporti di backup quando le rappresentazioni o i frammenti interi non sono disponibili.