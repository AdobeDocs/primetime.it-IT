---
description: La gestione del failover si verifica quando una playlist di varianti presenta più rappresentazioni per lo stesso bit rate e una delle rappresentazioni smette di funzionare. Il TVSDK passa tra le rappresentazioni.
title: Failover
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 0%

---


# Failover{#failover}

La gestione del failover si verifica quando una playlist di varianti presenta più rappresentazioni per lo stesso bit rate e una delle rappresentazioni smette di funzionare. Il TVSDK passa tra le rappresentazioni.

L&#39;esempio seguente mostra una playlist variante con URL di failover con lo stesso bit rate:

```
#EXTM3U
#EXT-X-STREAM-INF:PROGRAM-ID=1, BANDWIDTH =700000
https://sj2slu225.corp.adobe.com:8090/_default_/_default_/livestream.m3u8   

#EXT-X-STREAM-INF:PROGRAM-ID=1, BANDWIDTH =700000
https://sj2slu225.corp.adobe.com:8091/_default_/_default_/livestream.m3u8
```

Quando TVSDK carica la playlist della variante, crea una coda che contiene gli URL per tutte le rappresentazioni del contenuto per lo stesso bit rate. Quando una richiesta di un URL non riesce, TVSDK utilizza l&#39;URL successivo dello stesso bit rate dalla coda di failover. In qualsiasi momento di errore specifico, TVSDK passa una volta in rassegna tutti gli URL disponibili fino a quando non ne trova uno che funziona correttamente o finché non ha tentato tutti gli URL disponibili. Se TVSDK ha tentato di tutti gli URL disponibili e nessuno degli URL funziona, TVSDK smette di provare a riprodurre il contenuto.

Il failover avviene solo a livello M3U8, il che significa:

* Per il VOD, il failover può verificarsi solo quando inizia a tentare di riprodurre e non dopo l&#39;avvio della riproduzione.
* Per lo streaming live, il failover può avvenire nel mezzo del flusso.

>[!TIP]
>
>TVSDK, invece del lettore Apple AV Foundation, fornisce la gestione del failover.

