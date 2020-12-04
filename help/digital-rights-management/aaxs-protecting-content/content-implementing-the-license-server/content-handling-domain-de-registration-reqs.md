---
seo-title: Gestione delle richieste di annullamento della registrazione del dominio
title: Gestione delle richieste di annullamento della registrazione del dominio
uuid: 6f056b2b-374d-4e4d-926a-68605b2c923b
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---


# Gestione delle richieste di cancellazione del dominio{#handling-domain-de-registration-requests}

Se l&#39;applicazione client deve lasciare un dominio, richiama l&#39;API ActionScript `DRMManager.removeFromDeviceGroup()` o l&#39;API iOS `leaveLicenseDomain()` per avviare il processo di deregistrazione del dominio. La deregistrazione del dominio è un processo in due fasi. Il client invia innanzitutto una richiesta di anteprima per la cancellazione della registrazione. Il server di dominio esamina la richiesta e determina se al client è consentito uscire dal dominio (se il computer non fa attualmente parte del dominio potrebbe essere restituito un errore). In seguito a una risposta corretta, il client elimina le credenziali del proprio dominio e tutte le licenze rilasciate a tale dominio, quindi invia una richiesta di annullamento della registrazione.

* La classe del gestore di richieste è `com.adobe.flashaccess.sdk.protocol.domain.DomainDeRegistrationHandler`
* La classe del messaggio di richiesta è `com.adobe.flashaccess.sdk.protocol.domain.DomainDeRegistrationRequestMessage`
* Se client e server supportano entrambi il protocollo versione 5, l’URL della richiesta è &quot;URL del server di dominio nei metadati: + &quot;/flashaccess/dereg/v4&quot;. In caso contrario, l’URL della richiesta è l’URL del server di dominio nei metadati &quot; + &quot;/flashaccess/dereg/v3&quot;

Durante l&#39;elaborazione delle richieste di cancellazione del dominio, il server utilizza `getRequestPhase()` per determinare se il client si trova nella fase di anteprima o di deregistrazione. Nella fase di anteprima, il server del dominio esamina la richiesta e determina se al client è consentito uscire dal dominio (la richiesta potrebbe essere rifiutata, ad esempio, se il computer non fa attualmente parte del dominio). Nella fase di deregistrazione, il server registra il fatto che il computer ha lasciato il dominio. Si consiglia vivamente al server di valutare la stessa logica nella richiesta di anteprima come nella richiesta di cancellazione effettiva per ridurre al minimo la possibilità che la seconda fase non riesca.
