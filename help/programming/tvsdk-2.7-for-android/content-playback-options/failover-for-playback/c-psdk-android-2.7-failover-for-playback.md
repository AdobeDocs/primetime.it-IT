---
description: Lo streaming via Internet richiede una connessione costante e stabile per riprodurre un flusso da un server remoto. Tuttavia, la variabilità della connessione Internet o della riproduzione in streaming di un visualizzatore impedisce la riproduzione remota di contenuti multimediali di qualità riprodotti localmente.
title: Riproduzione e failover
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---


# Panoramica {#playback-and-failover-overview}

Lo streaming via Internet richiede una connessione costante e stabile per riprodurre un flusso da un server remoto. Tuttavia, la variabilità della connessione Internet o della riproduzione in streaming di un visualizzatore impedisce la riproduzione remota di contenuti multimediali di qualità riprodotti localmente.

>[!IMPORTANT]
>
>Primetime non è in grado di proteggere da guasti come un&#39;interruzione dell&#39;ISP o una disconnessione del cavo.

Lo streaming di Primetime fornisce una protezione di failover per proteggere la riproduzione da alcuni guasti del server remoto o da guasti operativi, il che migliora l&#39;esperienza di visualizzazione. Nonostante i problemi di trasmissione, TVSDK implementa la protezione del failover per ridurre al minimo le interruzioni di riproduzione e ottenere una riproduzione senza soluzione di continuità. Il lettore video passa automaticamente a un set di file multimediali di backup quando non sono disponibili interi rendering o frammenti.