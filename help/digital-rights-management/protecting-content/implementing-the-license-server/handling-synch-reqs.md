---
title: Gestire le richieste di sincronizzazione
description: Gestire le richieste di sincronizzazione
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%

---


# Gestire le richieste di sincronizzazione {#handle-synchronization-requests}

Se una licenza specifica i requisiti di sincronizzazione [Requisiti per la sincronizzazione,](../../protecting-content/introduction/usage-rules/authentication/synchronization.md) il client invia periodicamente le richieste di sincronizzazione al server in base alla frequenza specificata nella licenza. Per abilitare i messaggi di sincronizzazione, imposta `SyncFrequencyRequirements` in una PlayRight.

* La classe del gestore richieste è `com.adobe.flashaccess.sdk.protocol.sync.SynchronizationHandler`
* La classe del messaggio di richiesta è `com.adobe.flashaccess.sdk.protocol.sync.SynchronizationRequestMessage`
* Se il protocollo di supporto client e server versione 5, l’URL della richiesta è &quot;URL del server licenze nei metadati: + &quot; [!DNL /flashaccess/sync/v4]&quot;. In caso contrario, l’URL della richiesta è &quot;URL del server licenze nei metadati&quot; + &quot; [!DNL /flashaccess/sync/v3]&quot;

I messaggi di sincronizzazione vengono utilizzati per sincronizzare l&#39;ora del client con l&#39;ora del server. Se le licenze sono incorporate nel contenuto e non è necessario recuperarle da un server licenze, la sincronizzazione dell&#39;ora del client è importante per evitare che il client modifichi il proprio orologio al fine di bypassare la scadenza della licenza.

I messaggi di sincronizzazione possono inoltre essere utilizzati per comunicare le informazioni sullo stato del client al server ( `getClientState()`) per il rilevamento del rollback.

Vedere [Protezione del ripristino](../../protecting-content/implementing-the-license-server/processing-drm-requests.md#rollback-detection).
