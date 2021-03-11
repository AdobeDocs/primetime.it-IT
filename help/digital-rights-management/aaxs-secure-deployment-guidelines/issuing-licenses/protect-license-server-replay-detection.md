---
title: Protezione a ripetizione
description: Protezione a ripetizione
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---


# Protezione di riproduzione{#replay-protection}

La protezione di ripetizione impedisce a un autore dell&#39;attacco di riprodurre un messaggio di richiesta di licenza e potenzialmente causa un attacco Denial-of-Service (DoS) contro il client (L&#39;attacco A *denial-of-service* è un tentativo da parte degli aggressori di impedire agli utenti legittimi di un servizio di utilizzare quel servizio). Ad esempio, un attacco di ripetizione utilizzando il contatore di rollback potrebbe essere utilizzato per &quot;ingannare&quot; il server licenze a pensare che il client DRM stia riportando indietro lo stato, causando una sospensione dell&#39;account.

Per ulteriori informazioni sulla protezione della riproduzione, consulta `AbstractRequestMessage.getMessageId()` il *Riferimento API di accesso agli Adobi*.
