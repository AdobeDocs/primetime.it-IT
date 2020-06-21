---
description: Se l'implementazione di Adobe Primetime DRM utilizza regole aziendali che richiedono al client di mantenere lo stato (ad esempio, l'intervallo della finestra di riproduzione), Adobe consiglia al server di tenere traccia del contatore di rollback e di utilizzare AIR o SWF per consentire l'elencazione.
seo-description: Se l'implementazione di Adobe Primetime DRM utilizza regole aziendali che richiedono al client di mantenere lo stato (ad esempio, l'intervallo della finestra di riproduzione), Adobe consiglia al server di tenere traccia del contatore di rollback e di utilizzare AIR o SWF per consentire l'elencazione.
seo-title: Rilevamento del rollback
title: Rilevamento del rollback
uuid: f161ed41-488a-478a-b6a8-468cf6d11e89
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---


# Rilevamento del rollback {#rollback-detection}

Se l&#39;implementazione di Adobe Primetime DRM utilizza regole aziendali che richiedono al client di mantenere lo stato (ad esempio, l&#39;intervallo della finestra di riproduzione), Adobe consiglia al server di tenere traccia del contatore di rollback e di utilizzare AIR o SWF per consentire l&#39;elencazione.

Il contatore di rollback viene inviato al server nella maggior parte delle richieste dal client. Se l&#39;implementazione di Primetime DRM non richiede il contatore di rollback, può essere ignorata. In caso contrario, Adobe consiglia al server di memorizzare l&#39;ID computer casuale, ottenuto utilizzando [MachineToken.getUniqueId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId()), e il valore del contatore corrente in un database.

Per ulteriori informazioni su come incrementare e tenere traccia del contatore di rollback, vedere Rilevamento [ClientState](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/ClientState.html) e Rollback.