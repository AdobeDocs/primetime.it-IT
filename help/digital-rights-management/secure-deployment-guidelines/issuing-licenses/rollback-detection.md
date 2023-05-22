---
description: Se l'implementazione di Adobe Primetime DRM utilizza regole aziendali che richiedono al client di mantenere lo stato (ad esempio, l'intervallo di intervallo della finestra di riproduzione), l'Adobe consiglia al server di tenere traccia del contatore di rollback e di utilizzare l'elenco Consentiti di AIR o SWF.
title: Rilevamento rollback
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---


# Rilevamento rollback {#rollback-detection}

Se l&#39;implementazione di Adobe Primetime DRM utilizza regole aziendali che richiedono al client di mantenere lo stato (ad esempio, l&#39;intervallo di intervallo della finestra di riproduzione), l&#39;Adobe consiglia al server di tenere traccia del contatore di rollback e di utilizzare l&#39;elenco Consentiti di AIR o SWF.

Il contatore di rollback viene inviato al server nella maggior parte delle richieste provenienti dal client. Se l’implementazione di Primetime DRM non richiede il contatore di rollback, questo può essere ignorato. In caso contrario, Adobe consiglia che il server memorizzi l’ID computer casuale, ottenuto utilizzando [MachineToken.getUniqueId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId())e il valore del contatore corrente in un database.

Per ulteriori informazioni su come incrementare e tenere traccia del contatore di rollback, vedere [ClientState](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/ClientState.html) e il rilevamento di rollback.