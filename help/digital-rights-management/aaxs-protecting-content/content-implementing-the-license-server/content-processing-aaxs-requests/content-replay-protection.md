---
title: Protezione dalla ripetizione
description: Protezione dalla ripetizione
copied-description: true
exl-id: dfb6d615-07d2-4303-82cc-10cfee4bb387
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 0%

---

# Protezione dalla ripetizione{#replay-protection}

Per la protezione dalla ripetizione, può essere prudente controllare se l’identificatore del messaggio è stato visto di recente chiamando `RequestMessageBase.getMessageId()`. In tal caso, l’autore dell’attacco potrebbe tentare di ripetere la richiesta, che dovrebbe essere negata. Per rilevare i tentativi di ripetizione, il server può memorizzare un elenco degli ID di messaggi visualizzati di recente e confrontare ogni richiesta in ingresso con l’elenco memorizzato nella cache. Per limitare il tempo di memorizzazione degli identificatori del messaggio, invoca `HandlerConfiguration.setTimestampTolerance()`. Se questa proprietà è impostata, l&#39;SDK negherà qualsiasi richiesta che presenti una marca temporale maggiore del numero di secondi specificato rispetto all&#39;ora del server.
