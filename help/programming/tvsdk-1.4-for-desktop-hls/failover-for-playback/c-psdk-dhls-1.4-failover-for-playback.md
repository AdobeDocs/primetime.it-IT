---
description: Lo streaming via Internet richiede una connessione costante e stabile per riprodurre un flusso da un server remoto. Tuttavia, la variabilità della connessione Internet o della riproduzione in streaming di un utente fa sì che la riproduzione remota possa non avere la qualità dei contenuti multimediali riprodotti localmente.
title: Riproduzione e failover
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 0%

---

# Panoramica {#playback-and-failover-overview}

Lo streaming via Internet richiede una connessione costante e stabile per riprodurre un flusso da un server remoto. Tuttavia, la variabilità della connessione Internet o della riproduzione in streaming di un utente fa sì che la riproduzione remota possa non avere la qualità dei contenuti multimediali riprodotti localmente.

Primetime non è in grado di proteggere da errori quali un&#39;interruzione del servizio ISP o la disconnessione di un cavo. Tuttavia, lo streaming di Primetime offre protezione da failover per proteggere la riproduzione da determinati guasti del server remoto o da errori operativi, migliorando l&#39;esperienza dei visualizzatori. TVSDK implementa la protezione di failover per ridurre al minimo le interruzioni della riproduzione e ottenere una riproduzione ottimale nonostante i problemi di trasmissione. Il lettore video passa automaticamente a un set di supporti di backup quando non sono disponibili rappresentazioni o frammenti interi.
