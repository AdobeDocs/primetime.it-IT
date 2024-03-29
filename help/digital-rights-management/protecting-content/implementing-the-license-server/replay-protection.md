---
title: Protezione dalla ripetizione
description: Protezione dalla ripetizione
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 0%

---


# Protezione dalla ripetizione{#replay-protection}

Per la protezione dalla ripetizione, è possibile verificare se l’identificatore del messaggio è stato visualizzato di recente chiamando `RequestMessageBase.getMessageId()`. In tal caso, l’autore dell’attacco potrebbe tentare di ripetere la richiesta, che dovrebbe essere negata. Per rilevare i tentativi di ripetizione, il server può memorizzare un elenco degli ID di messaggi visualizzati di recente e confrontare ogni richiesta in ingresso con l’elenco memorizzato nella cache. Per limitare il tempo di memorizzazione degli identificatori del messaggio, invoca `HandlerConfiguration.setTimestampTolerance()`. Se questa proprietà è impostata, l&#39;SDK nega quindi qualsiasi richiesta che presenti una marca temporale superiore al numero di secondi specificati fuori dall&#39;ora del server.
