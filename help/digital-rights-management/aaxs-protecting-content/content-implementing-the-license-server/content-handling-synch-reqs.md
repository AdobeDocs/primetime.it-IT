---
title: Gestione delle richieste di sincronizzazione
description: Gestione delle richieste di sincronizzazione
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 0%

---


# Gestione delle richieste di sincronizzazione{#handling-synchronization-requests}

. Se una licenza specifica i requisiti di sincronizzazione ([Requisiti per la sincronizzazione](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-time-based-rules/content-time-based-rules-defining.md#requirements-for-synchronization)), il client invia periodicamente le richieste di sincronizzazione al server, in base alla frequenza specificata nella licenza. Per abilitare i messaggi di sincronizzazione, imposta SyncFrequencyRequirements in a PlayRight.

* La classe del gestore richieste è `com.adobe.flashaccess.sdk.protocol.sync.SynchronizationHandler`
* La classe del messaggio di richiesta è `com.adobe.flashaccess.sdk.protocol.sync.SynchronizationRequestMessage`
* Se il protocollo di supporto client e server versione 5, l’URL della richiesta è &quot;URL del server licenze nei metadati: + &quot;/flashaccess/sync/v4&quot;. In caso contrario, l&#39;URL della richiesta è &quot;URL del server licenze nei metadati&quot; + &quot;/flashaccess/sync/v3&quot;

I messaggi di sincronizzazione vengono utilizzati per sincronizzare l&#39;ora del client con l&#39;ora del server. Se le licenze sono incorporate nel contenuto e non è necessario recuperarle da un server licenze, la sincronizzazione dell&#39;ora del client è importante per evitare che il client modifichi il proprio orologio al fine di bypassare la scadenza della licenza.

I messaggi di sincronizzazione possono inoltre essere utilizzati per comunicare le informazioni sullo stato del client al server ( `getClientState()`) per il rilevamento del rollback. Vedere [Protezione del ripristino](../../aaxs-protecting-content/content-implementing-the-license-server/content-processing-aaxs-requests/content-rollback-detection.md).