---
description: La protezione della ripetizione impedisce a un utente malintenzionato di riprodurre un messaggio di richiesta di licenza e può causare un attacco Denial of Service (DoS) contro il client.
title: Protezione dalla ripetizione
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 0%

---


# Protezione dalla ripetizione{#replay-protection}

La protezione della ripetizione impedisce a un utente malintenzionato di riprodurre un messaggio di richiesta di licenza e può causare un attacco Denial of Service (DoS) contro il client.

Un attacco DoS è un tentativo da parte degli aggressori di impedire agli utenti legittimi di un servizio di utilizzare tale servizio. Ad esempio, un attacco di ripetizione che utilizza il contatore di rollback potrebbe essere utilizzato per &quot;ingannare&quot; il server licenze a pensare che il client DRM abbia ripristinato il suo stato, causando una sospensione dell’account.

Per ulteriori informazioni sulla protezione dalla ripetizione, consulta [ AbstractRequestMessage.getMessageId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/AbstractRequestMessage.html#getMessageId()).
