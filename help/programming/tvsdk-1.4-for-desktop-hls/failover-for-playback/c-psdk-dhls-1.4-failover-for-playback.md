---
description: Lo streaming via Internet richiede una connessione costante e stabile per riprodurre un flusso da un server remoto. Tuttavia, la variabilità della connessione Internet o della riproduzione in streaming di un utente fa sì che la riproduzione remota possa non avere la qualità dei contenuti multimediali riprodotti localmente.
title: Riproduzione e failover
exl-id: 45693d0b-a5fb-4716-a410-ac323950f40b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 0%

---

# Panoramica {#playback-and-failover-overview}

Lo streaming via Internet richiede una connessione costante e stabile per riprodurre un flusso da un server remoto. Tuttavia, la variabilità della connessione Internet o della riproduzione in streaming di un utente fa sì che la riproduzione remota possa non avere la qualità dei contenuti multimediali riprodotti localmente.

Primetime non è in grado di proteggere da errori quali un&#39;interruzione del servizio ISP o la disconnessione di un cavo. Tuttavia, lo streaming di Primetime offre protezione da failover per proteggere la riproduzione da determinati guasti del server remoto o da errori operativi, migliorando l&#39;esperienza dei visualizzatori. TVSDK implementa la protezione di failover per ridurre al minimo le interruzioni della riproduzione e ottenere una riproduzione ottimale nonostante i problemi di trasmissione. Il lettore video passa automaticamente a un set di supporti di backup quando non sono disponibili rappresentazioni o frammenti interi.
