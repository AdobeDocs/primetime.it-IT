---
title: Gestire le richieste di sincronizzazione
description: Gestire le richieste di sincronizzazione
copied-description: true
exl-id: b19245e3-19ae-4dd4-9e5e-6956feb91334
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%

---

# Gestire le richieste di sincronizzazione {#handle-synchronization-requests}

Se una licenza specifica i requisiti di sincronizzazione  [Requisiti per la sincronizzazione,](../../protecting-content/introduction/usage-rules/authentication/synchronization.md) il client invia periodicamente le richieste di sincronizzazione al server, in base alla frequenza specificata nella licenza. Per abilitare i messaggi di sincronizzazione, impostare `SyncFrequencyRequirements` in un PlayRight.

* La classe del gestore richieste è `com.adobe.flashaccess.sdk.protocol.sync.SynchronizationHandler`
* La classe del messaggio di richiesta è `com.adobe.flashaccess.sdk.protocol.sync.SynchronizationRequestMessage`
* Se sia il client che il server supportano la versione 5 del protocollo, l’URL della richiesta è &quot;License Server URL in metadata: + &quot; [!DNL /flashaccess/sync/v4]&quot;. In caso contrario, l’URL della richiesta è &quot;License Server URL in metadata&quot; + &quot; [!DNL /flashaccess/sync/v3]&quot;

I messaggi di sincronizzazione vengono utilizzati per sincronizzare l&#39;ora del client con l&#39;ora del server. Se le licenze sono incorporate nel contenuto e non è necessario recuperarle da un server licenze, è importante sincronizzare l&#39;ora del client per evitare che modifichi l&#39;orologio in modo da evitare la scadenza della licenza.

I messaggi di sincronizzazione possono essere utilizzati anche per comunicare le informazioni sullo stato del client al server ( `getClientState()`) per il rilevamento del rollback.

Consulta [Protezione rollback](../../protecting-content/implementing-the-license-server/processing-drm-requests.md#rollback-detection).
