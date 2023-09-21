---
title: Gestione delle richieste di sincronizzazione
description: Gestione delle richieste di sincronizzazione
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 0%

---

# Gestione delle richieste di sincronizzazione{#handling-synchronization-requests}

. Se una licenza specifica i requisiti di sincronizzazione ([Requisiti per la sincronizzazione](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-time-based-rules/content-time-based-rules-defining.md#requirements-for-synchronization)), il client invierà periodicamente richieste di sincronizzazione al server, in base alla frequenza specificata nella licenza. Per abilitare i messaggi di sincronizzazione, impostare SyncFrequencyRequirements in un oggetto PlayRight.

* La classe del gestore richieste è `com.adobe.flashaccess.sdk.protocol.sync.SynchronizationHandler`
* La classe del messaggio di richiesta è `com.adobe.flashaccess.sdk.protocol.sync.SynchronizationRequestMessage`
* Se sia il client che il server supportano la versione 5 del protocollo, l&#39;URL della richiesta è &quot;License Server URL in metadata: + &quot;/flashaccess/sync/v4&quot;. In caso contrario, l’URL della richiesta è &quot;License Server URL in metadata&quot; + &quot;/flashaccess/sync/v3&quot;

I messaggi di sincronizzazione vengono utilizzati per sincronizzare l&#39;ora del client con l&#39;ora del server. Se le licenze sono incorporate nel contenuto e non è necessario recuperarle da un server licenze, è importante sincronizzare l&#39;ora del client per evitare che modifichi l&#39;orologio in modo da evitare la scadenza della licenza.

I messaggi di sincronizzazione possono essere utilizzati anche per comunicare le informazioni sullo stato del client al server ( `getClientState()`) per il rilevamento del rollback. Consulta [Protezione rollback](../../aaxs-protecting-content/content-implementing-the-license-server/content-processing-aaxs-requests/content-rollback-detection.md).
