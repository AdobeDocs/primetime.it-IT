---
seo-title: Protezione di ripetizione
title: Protezione di ripetizione
uuid: c737998a-9c33-48b4-b741-91106697d71f
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Protezione di ripetizione{#replay-protection}

Per la protezione di ripetizione, potrebbe essere utile verificare se l&#39;identificatore del messaggio è stato visualizzato di recente chiamando `RequestMessageBase.getMessageId()`. In tal caso, un utente malintenzionato potrebbe tentare di riprodurre nuovamente la richiesta, cosa che dovrebbe essere negata. Per rilevare i tentativi di riproduzione, il server può memorizzare un elenco di ID messaggio visti di recente e controllare ogni richiesta in entrata rispetto all&#39;elenco memorizzato nella cache. Per limitare il tempo necessario per memorizzare gli identificatori del messaggio, chiama `HandlerConfiguration.setTimestampTolerance()`. Se questa proprietà è impostata, l’SDK nega quindi qualsiasi richiesta con marca temporale per più di un numero specificato di secondi dall’ora del server.
