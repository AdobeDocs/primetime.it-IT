---
seo-title: Protezione di ripetizione
title: Protezione di ripetizione
uuid: 5e6488e6-0834-4dcf-bc26-55019f5db320
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Protezione di ripetizione{#replay-protection}

La protezione contro la ripetizione impedisce a un aggressore di riprodurre un messaggio di richiesta di licenza e potrebbe causare un attacco di tipo Denial of Service (DoS) contro il client (un attacco *di tipo Denial of Service* è un tentativo da parte degli aggressori di impedire che utenti legittimi di un servizio utilizzino tale servizio). Ad esempio, un attacco di ripetizione utilizzando il contatore di rollback potrebbe essere utilizzato per &quot;indurre&quot; il server licenze a pensare che il client DRM stia ripristinando il proprio stato, causando una sospensione dell&#39;account.

Per ulteriori informazioni sulla protezione contro `AbstractRequestMessage.getMessageId()` la riproduzione ripetuta, consultare il documento di riferimento *per le API di* Adobe Access.
