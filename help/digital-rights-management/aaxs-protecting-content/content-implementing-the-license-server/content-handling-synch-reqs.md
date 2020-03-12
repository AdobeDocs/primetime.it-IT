---
seo-title: Gestione delle richieste di sincronizzazione
title: Gestione delle richieste di sincronizzazione
uuid: 37b2db09-4c09-4216-874b-b570a84569b6
translation-type: tm+mt
source-git-commit: 53654b740b03c6a79394d30704a41186d4655237

---


# Gestione delle richieste di sincronizzazione{#handling-synchronization-requests}

. Se una licenza specifica i requisiti di sincronizzazione ([Requisiti per la sincronizzazione](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-time-based-rules/content-time-based-rules-defining.md#requirements-for-synchronization)), il client invierà periodicamente al server richieste di sincronizzazione, in base alla frequenza specificata nella licenza. Per abilitare i messaggi di sincronizzazione, imposta SyncFrequencyRequirements in una PlayRight.

* La classe gestore di richieste è `com.adobe.flashaccess.sdk.protocol.sync.SynchronizationHandler`
* La classe del messaggio di richiesta è `com.adobe.flashaccess.sdk.protocol.sync.SynchronizationRequestMessage`
* Se client e server supportano entrambi il protocollo versione 5, l’URL della richiesta è &quot;URL server licenze nei metadati: + &quot;/flashaccess/sync/v4&quot;. In caso contrario, l’URL della richiesta è &quot;URL del server delle licenze nei metadati&quot; + &quot;/flashaccess/sync/v3&quot;

I messaggi di sincronizzazione vengono utilizzati per sincronizzare l&#39;ora del client con quella del server. Se le licenze sono incorporate nel contenuto e non è necessario recuperarle da un server licenze, la sincronizzazione dell&#39;ora del client è importante per evitare che il client modifichi il proprio orologio al fine di evitare la scadenza della licenza.

I messaggi di sincronizzazione possono essere utilizzati anche per comunicare le informazioni sullo stato del client al server ( `getClientState()`) per il rilevamento del rollback. Vedere Protezione [](../../aaxs-protecting-content/content-implementing-the-license-server/content-processing-aaxs-requests/content-rollback-detection.md)ripristino.