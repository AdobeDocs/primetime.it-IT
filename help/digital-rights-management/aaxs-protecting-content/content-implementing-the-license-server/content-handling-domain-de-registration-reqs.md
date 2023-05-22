---
title: Gestione delle richieste di annullamento della registrazione dei domini
description: Gestione delle richieste di annullamento della registrazione dei domini
copied-description: true
exl-id: f29507b5-d32a-4b22-a02e-6701b86db133
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---

# Gestione delle richieste di annullamento della registrazione dei domini{#handling-domain-de-registration-requests}

Se l’applicazione client deve lasciare un dominio, richiama `DRMManager.removeFromDeviceGroup()`API ACTIONSCRIPT o `leaveLicenseDomain()` API di iOS per avviare il processo di annullamento della registrazione del dominio. La cancellazione del dominio è un processo in due fasi. Il client invia prima una richiesta di anteprima di annullamento della registrazione. Il server di dominio esamina la richiesta e determina se al client è consentito lasciare il dominio. Se il computer non fa attualmente parte del dominio, è possibile che venga restituito un errore. In caso di esito positivo, il client elimina le credenziali del dominio e le eventuali licenze rilasciate a tale dominio, quindi invia una richiesta di annullamento della registrazione.

* La classe del gestore richieste è `com.adobe.flashaccess.sdk.protocol.domain.DomainDeRegistrationHandler`
* La classe del messaggio di richiesta è `com.adobe.flashaccess.sdk.protocol.domain.DomainDeRegistrationRequestMessage`
* Se sia il client che il server supportano la versione 5 del protocollo, l’URL della richiesta è &quot;Domain Server URL in metadata: + &quot;/flashaccess/dereg/v4&quot;. In caso contrario, l’URL della richiesta è URL del server di dominio nei metadati&quot; + &quot;/flashaccess/dereg/v3&quot;

Durante l’elaborazione delle richieste di cancellazione del dominio, il server utilizza `getRequestPhase()` per determinare se il client si trova nella fase di anteprima o di annullamento della registrazione. Nella fase di anteprima, il server di dominio esamina la richiesta e determina se al client è consentito lasciare il dominio (la richiesta può essere rifiutata, ad esempio, se il computer non fa attualmente parte del dominio). Nella fase di annullamento della registrazione, il server registra il fatto che il computer ha lasciato il dominio. Si consiglia vivamente al server di valutare nella richiesta di anteprima la stessa logica utilizzata nella richiesta di annullamento della registrazione per ridurre al minimo la possibilità che la seconda fase non riesca.
