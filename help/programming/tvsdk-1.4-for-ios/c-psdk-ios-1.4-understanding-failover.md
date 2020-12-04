---
description: La gestione del failover si verifica quando una playlist di variante ha più rappresentazioni per lo stesso bitrate e una delle rappresentazioni non funziona più. Il TVSDK passa da una rappresentazione all'altra.
seo-description: La gestione del failover si verifica quando una playlist di variante ha più rappresentazioni per lo stesso bitrate e una delle rappresentazioni non funziona più. Il TVSDK passa da una rappresentazione all'altra.
seo-title: Failover
title: Failover
uuid: 53cf611f-59e6-4728-a287-b98907d7f7bb
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---


# Failover{#failover}

La gestione del failover si verifica quando una playlist di variante ha più rappresentazioni per lo stesso bitrate e una delle rappresentazioni non funziona più. Il TVSDK passa da una rappresentazione all&#39;altra.

L&#39;esempio seguente mostra una playlist di variante con URL di failover con lo stesso bitrate:

```
#EXTM3U
#EXT-X-STREAM-INF:PROGRAM-ID=1, BANDWIDTH =700000
https://sj2slu225.corp.adobe.com:8090/_default_/_default_/livestream.m3u8   

#EXT-X-STREAM-INF:PROGRAM-ID=1, BANDWIDTH =700000
https://sj2slu225.corp.adobe.com:8091/_default_/_default_/livestream.m3u8
```

Quando TVSDK carica la playlist della variante, crea una coda che contiene gli URL per tutte le rappresentazioni del contenuto per lo stesso bitrate. Quando una richiesta di URL non riesce, TVSDK utilizza l’URL successivo dello stesso bitrate dalla coda di failover. In qualsiasi momento di errore specifico, TVSDK passa in rassegna tutti gli URL disponibili fino a quando non ne trova uno che funzioni correttamente o finché non abbia provato tutti gli URL disponibili. Se TVSDK ha provato a visualizzare tutti gli URL disponibili e nessuno degli URL funziona, TVSDK smette di provare a riprodurre il contenuto.

Il failover avviene solo a livello M3U8, il che significa:

* Per il VOD, il failover può avvenire solo quando inizia a tentare di riprodurre e non dopo che ha iniziato la riproduzione.
* Per lo streaming live, il failover può avvenire al centro del flusso.

>[!TIP]
>
>TVSDK, invece del lettore Apple AV Foundation, fornisce la gestione del failover.

