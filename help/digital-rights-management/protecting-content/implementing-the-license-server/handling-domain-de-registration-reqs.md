---
title: Gestire le richieste di cancellazione del dominio
description: Gestire le richieste di cancellazione del dominio
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---


# Gestire le richieste di cancellazione del dominio {#handle-domain-de-registration-requests}

Se l’applicazione client deve lasciare un dominio, richiama l’ API `DRMManager.removeFromDeviceGroup()`ActionScript o l’ API iOS `leaveLicenseDomain()` per avviare il processo di cancellazione del dominio. La deregistrazione del dominio è un processo in due fasi. Il client invia prima una richiesta di anteprima di cancellazione della registrazione. Il server di dominio esamina la richiesta e determina se al client è consentito lasciare il dominio. È possibile che venga restituito un errore se il computer non fa attualmente parte del dominio . In seguito a una risposta corretta, il client elimina le credenziali del dominio e le licenze rilasciate a tale dominio. Invia quindi una richiesta di cancellazione della registrazione.

* La classe del gestore richieste è `com.adobe.flashaccess.sdk.protocol.domain.DomainDeRegistrationHandler`
* La classe del messaggio di richiesta è `com.adobe.flashaccess.sdk.protocol.domain.DomainDeRegistrationRequestMessage`
* Se versione 5 del protocollo di supporto client e server, l’URL della richiesta è &quot;URL del server di dominio nei metadati: + &quot; [!DNL /flashaccess/dereg/v4]&quot;. In caso contrario, l&#39;URL della richiesta è l&#39;URL del server di dominio nei metadati &quot; + &quot; [!DNL /flashaccess/dereg/v3]&quot;

Durante l’elaborazione delle richieste di cancellazione del dominio, il server utilizza `getRequestPhase()` per determinare se il client si trova nella fase di anteprima o di cancellazione della registrazione. Nella fase di anteprima, il server di dominio esamina la richiesta e determina se al client è consentito lasciare il dominio perché la richiesta potrebbe essere negata; ad esempio, la richiesta potrebbe essere negata se il computer non fa attualmente parte del dominio . Nella fase di deregistrazione, il server registra il fatto che il computer ha lasciato il dominio. Si consiglia vivamente al server di valutare la stessa logica nella richiesta di anteprima come nella richiesta di cancellazione effettiva per ridurre al minimo il rischio di errore della seconda fase.
