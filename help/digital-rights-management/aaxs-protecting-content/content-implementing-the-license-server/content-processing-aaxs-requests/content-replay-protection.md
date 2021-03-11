---
title: Protezione a ripetizione
description: Protezione a ripetizione
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 0%

---


# Protezione di riproduzione{#replay-protection}

Per la protezione di ripetizione, può essere prudente verificare se l&#39;identificatore del messaggio è stato visualizzato di recente chiamando `RequestMessageBase.getMessageId()`. In tal caso, l&#39;autore dell&#39;attacco potrebbe tentare di riprodurre nuovamente la richiesta, che dovrebbe essere negata. Per rilevare i tentativi di ripetizione, il server può memorizzare un elenco di ID messaggio visualizzati di recente e controllare ogni richiesta in arrivo rispetto all’elenco memorizzato nella cache. Per limitare il tempo necessario alla memorizzazione degli identificatori del messaggio, invoca `HandlerConfiguration.setTimestampTolerance()`. Se questa proprietà è impostata, l&#39;SDK nega qualsiasi richiesta con una marca temporale superiore al numero specificato di secondi trascorsi dal tempo del server.
