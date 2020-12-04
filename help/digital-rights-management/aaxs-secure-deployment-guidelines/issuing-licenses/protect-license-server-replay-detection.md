---
seo-title: Protezione di ripetizione
title: Protezione di ripetizione
uuid: 5e6488e6-0834-4dcf-bc26-55019f5db320
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---


# Protezione riproduzione{#replay-protection}

La protezione contro la ripetizione impedisce a un aggressore di riprodurre un messaggio di richiesta di licenza e potrebbe causare un attacco di negazione del servizio (DoS) contro il client (A *negazione del servizio* è un tentativo da parte degli aggressori di impedire l&#39;uso di tale servizio da parte degli utenti legittimi.) Ad esempio, un attacco di ripetizione utilizzando il contatore di rollback potrebbe essere utilizzato per &quot;indurre&quot; il server licenze a pensare che il client DRM stia ripristinando il proprio stato, causando una sospensione dell&#39;account.

Per ulteriori informazioni sulla protezione della riproduzione, vedere `AbstractRequestMessage.getMessageId()` il *Riferimento API di accesso ai Adobi*.
