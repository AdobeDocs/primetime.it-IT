---
description: La gestione del failover si verifica quando una playlist di varianti presenta più copie trasformate per la stessa velocità bit e una di esse smette di funzionare. Il TVSDK passa da un rendering all’altro.
title: Failover
exl-id: 8c215e2b-e601-4991-a66f-0e810176a511
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 0%

---

# Failover{#failover}

La gestione del failover si verifica quando una playlist di varianti presenta più copie trasformate per la stessa velocità bit e una di esse smette di funzionare. Il TVSDK passa da un rendering all’altro.

L’esempio seguente mostra una playlist di varianti con URL di failover della stessa velocità in bit:

```
#EXTM3U
#EXT-X-STREAM-INF:PROGRAM-ID=1, BANDWIDTH =700000
https://sj2slu225.corp.adobe.com:8090/_default_/_default_/livestream.m3u8   

#EXT-X-STREAM-INF:PROGRAM-ID=1, BANDWIDTH =700000
https://sj2slu225.corp.adobe.com:8091/_default_/_default_/livestream.m3u8
```

Quando TVSDK carica la playlist delle varianti, crea una coda che contiene gli URL di tutte le rappresentazioni del contenuto con la stessa velocità bit. Quando una richiesta di un URL non riesce, TVSDK utilizza l’URL successivo con la stessa velocità bit dalla coda di failover. In qualsiasi momento di errore specifico, TVSDK scorre una volta tra tutti gli URL disponibili fino a quando non ne trova uno che funziona correttamente o fino a quando non ha tentato tutti gli URL disponibili. Se TVSDK ha tentato di usare tutti gli URL disponibili e nessuno di essi funziona, TVSDK smette di provare a riprodurre il contenuto.

Il failover si verifica solo a livello di M3U8, il che significa:

* Per VOD, il failover può verificarsi solo quando inizia a tentare di riprodurre e non dopo l&#39;avvio della riproduzione.
* Per lo streaming live, il failover può avvenire nel mezzo del flusso.

>[!TIP]
>
>TVSDK, anziché Apple AV Foundation Player, consente la gestione del failover.
