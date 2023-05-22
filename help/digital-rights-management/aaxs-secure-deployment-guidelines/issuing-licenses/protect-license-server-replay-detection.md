---
title: Protezione dalla ripetizione
description: Protezione dalla ripetizione
copied-description: true
exl-id: 1e6ad730-b150-4e8f-9e79-e6b4fe006bf8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---

# Protezione dalla ripetizione{#replay-protection}

La protezione della ripetizione impedisce a un utente malintenzionato di riprodurre un messaggio di richiesta di licenza e può causare un attacco Denial of Service (DoS) contro il client (A *denial-of-service* l&#39;attacco è un tentativo da parte degli aggressori di impedire agli utenti legittimi di un servizio di utilizzare tale servizio). Ad esempio, un attacco di ripetizione utilizzando il contatore di rollback potrebbe essere utilizzato per &quot;ingannare&quot; il server licenze a pensare che il client DRM stia ripristinando il proprio stato, causando una sospensione dell’account.

Per ulteriori informazioni sulla protezione dalla ripetizione, consulta `AbstractRequestMessage.getMessageId()` il *Riferimento API per l’accesso agli Adobi*.
