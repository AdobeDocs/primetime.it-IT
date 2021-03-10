---
description: Se l'implementazione di Adobe Primetime DRM utilizza regole aziendali che richiedono al client di mantenere lo stato (ad esempio, l'intervallo della finestra di riproduzione), l'Adobe consiglia al server di tenere traccia del contatore di rollback e di utilizzare l'elenco Consentiti in AIR o SWF.
title: Rilevamento del ripristino
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---


# Rilevamento di ripristino {#rollback-detection}

Se l&#39;implementazione di Adobe Primetime DRM utilizza regole aziendali che richiedono al client di mantenere lo stato (ad esempio, l&#39;intervallo della finestra di riproduzione), l&#39;Adobe consiglia al server di tenere traccia del contatore di rollback e di utilizzare l&#39;elenco Consentiti in AIR o SWF.

Il contatore di rollback viene inviato al server nella maggior parte delle richieste dal client. Se l&#39;implementazione di Primetime DRM non richiede il contatore di rollback, può essere ignorato. In caso contrario, Adobe consiglia al server di memorizzare l&#39;ID computer casuale, ottenuto utilizzando [MachineToken.getUniqueId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId()), e il valore del contatore corrente in un database.

Per ulteriori informazioni su come incrementare e tenere traccia del contatore di rollback, vedere [ClientState](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/ClientState.html) e Rilevamento di rollback.