---
description: La protezione di ripetizione impedisce a un aggressore di riprodurre un messaggio di richiesta di licenza e potrebbe causare un attacco DoS (Denial of Service) contro il client.
seo-description: La protezione di ripetizione impedisce a un aggressore di riprodurre un messaggio di richiesta di licenza e potrebbe causare un attacco DoS (Denial of Service) contro il client.
seo-title: Protezione di ripetizione
title: Protezione di ripetizione
uuid: 93749dd3-a42c-4866-ac54-1b20d6683c42
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 0%

---


# Protezione riproduzione{#replay-protection}

La protezione di ripetizione impedisce a un aggressore di riprodurre un messaggio di richiesta di licenza e potrebbe causare un attacco DoS (Denial of Service) contro il client.

Un attacco DoS è un tentativo da parte degli aggressori di impedire agli utenti legittimi di un servizio di utilizzare tale servizio. Ad esempio, un attacco di ripetizione che utilizza il contatore di rollback potrebbe essere utilizzato per &quot;ingannare&quot; il server licenze a pensare che il client DRM abbia ripristinato il suo stato, causando una sospensione dell&#39;account.

Per ulteriori informazioni sulla protezione della riproduzione, vedere [ AbstractRequestMessage.getMessageId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/AbstractRequestMessage.html#getMessageId()).
