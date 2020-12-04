---
seo-title: Protezione di ripetizione
title: Protezione di ripetizione
uuid: 75f2be65-b2fc-428a-b853-34a4b30960ce
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 0%

---


# Protezione riproduzione{#replay-protection}

Per la protezione della riproduzione, può essere prudente verificare se l&#39;identificatore del messaggio è stato visualizzato di recente chiamando `RequestMessageBase.getMessageId()`. In tal caso, un utente malintenzionato potrebbe tentare di riprodurre nuovamente la richiesta, cosa che dovrebbe essere negata. Per rilevare i tentativi di ripetizione, il server può memorizzare un elenco di ID messaggio visti di recente e controllare ogni richiesta in entrata rispetto all&#39;elenco memorizzato nella cache. Per limitare il tempo di memorizzazione degli identificatori del messaggio, chiamare `HandlerConfiguration.setTimestampTolerance()`. Se questa proprietà è impostata, l’SDK negherà qualsiasi richiesta con marca temporale superiore al numero specificato di secondi dall’ora del server.
