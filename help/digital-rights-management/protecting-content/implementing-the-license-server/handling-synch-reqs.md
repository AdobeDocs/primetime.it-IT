---
seo-title: Gestione delle richieste di sincronizzazione
title: Gestione delle richieste di sincronizzazione
uuid: e2623afb-7a57-402d-a8a1-07bcf6324d41
translation-type: tm+mt
source-git-commit: eed2ed2512c2c462cd43637d83d80bf9a5c0d490
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%

---


# Gestire le richieste di sincronizzazione {#handle-synchronization-requests}

Se una licenza specifica i requisiti di sincronizzazione [Requisiti per la sincronizzazione,](../../protecting-content/introduction/usage-rules/authentication/synchronization.md) il client invia periodicamente al server richieste di sincronizzazione, in base alla frequenza specificata nella licenza. Per abilitare i messaggi di sincronizzazione, impostare `SyncFrequencyRequirements` in una PlayRight.

* La classe del gestore di richieste è `com.adobe.flashaccess.sdk.protocol.sync.SynchronizationHandler`
* La classe del messaggio di richiesta è `com.adobe.flashaccess.sdk.protocol.sync.SynchronizationRequestMessage`
* Se client e server supportano entrambi il protocollo versione 5, l’URL della richiesta è &quot;URL server licenze nei metadati: + &quot; [!DNL /flashaccess/sync/v4]&quot;. In caso contrario, l&#39;URL della richiesta è &quot;URL del server delle licenze nei metadati&quot; + &quot; [!DNL /flashaccess/sync/v3]&quot;

I messaggi di sincronizzazione vengono utilizzati per sincronizzare l&#39;ora del client con quella del server. Se le licenze sono incorporate nel contenuto e non è necessario recuperarle da un server licenze, la sincronizzazione dell&#39;ora del client è importante per evitare che il client modifichi il proprio orologio al fine di evitare la scadenza della licenza.

I messaggi di sincronizzazione possono essere utilizzati anche per comunicare le informazioni sullo stato del client al server ( `getClientState()`) per il rilevamento del rollback.

Vedere [Protezione ripristino](../../protecting-content/implementing-the-license-server/processing-drm-requests.md#rollback-detection).
