---
title: Protezione dalla ripetizione
description: Protezione dalla ripetizione
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---

# Protezione dalla ripetizione{#replay-protection}

La protezione della ripetizione impedisce a un utente malintenzionato di riprodurre un messaggio di richiesta di licenza e può causare un attacco Denial of Service (DoS) contro il client (A *denial-of-service* l&#39;attacco è un tentativo da parte degli aggressori di impedire agli utenti legittimi di un servizio di utilizzare tale servizio). Ad esempio, un attacco di ripetizione utilizzando il contatore di rollback potrebbe essere utilizzato per &quot;ingannare&quot; il server licenze a pensare che il client DRM stia ripristinando il proprio stato, causando una sospensione dell’account.

Per ulteriori informazioni sulla protezione dalla ripetizione, consulta `AbstractRequestMessage.getMessageId()` il *Riferimento API per l’accesso agli Adobi*.
