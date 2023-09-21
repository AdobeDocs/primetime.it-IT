---
title: Gestire le richieste di registrazione del dominio
description: Gestire le richieste di registrazione del dominio
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 0%

---

# Gestire le richieste di registrazione del dominio {#handle-domain-registration-requests}

Se i metadati DRM indicano che è necessaria la registrazione del dominio per riprodurre il contenuto, l’applicazione client deve richiamare `DRMManager.addToDeviceGroup()` API ACTIONSCRIPT o `joinLicenseDomain()` API iOS. Se il client non si è ancora registrato con il server di dominio specificato o se l&#39;applicazione sta forzando un nuovo join, viene inviata una richiesta di registrazione del dominio. Il server di dominio determina se al client è consentito aggiungere un dominio e rilascia una o più credenziali di dominio al client.

* La classe del gestore richieste è `com.adobe.flashaccess.sdk.protocol.domain.DomainRegistrationHandler`
* La classe del messaggio di richiesta è `com.adobe.flashaccess.sdk.protocol.domain.DomainRegistrationRequestMessage`
* Se sia il client che il server supportano la versione 5 del protocollo, l’URL della richiesta è &quot;URL del server di dominio nei metadati: + &quot; [!DNL /flashaccess/domain/v4]&quot;. In caso contrario, l’URL della richiesta è l’URL del server di dominio nei metadati&quot; + &quot; [!DNL /flashaccess/domain/v3]&quot;

Quando si inizializzano le `DomainRegistrationHandler`, è necessario specificare l’URL del server di dominio. Questo URL viene quindi incluso nei token di dominio rilasciati dal gestore per indicare al server di dominio che il token è stato rilasciato. L&#39;URL deve corrispondere all&#39;URL del server di dominio specificato in qualsiasi criterio DRM che richiede la registrazione del dominio con il server.

Per determinare se al client è consentito aggiungere il dominio, il server può esaminare le informazioni relative al computer e all&#39;utente nella richiesta. Il server può inoltre determinare a quale dominio il client può partecipare.

>[!NOTE]
>
>Un client può essere membro di un solo dominio per URL del server di dominio. Se il computer dispone già di un token di dominio per questo URL del server di dominio, la richiesta di registrazione del dominio include il nome di dominio corrente ( `getRequestDomainName()`).

Per una richiesta di aggiunta di nuovo dominio, il server di dominio deve restituire il set corrente di credenziali di dominio per il dominio o restituire un errore. Il server di dominio non può restituire le credenziali di dominio per un dominio diverso.

Consulta [Utilizzo degli identificatori macchina](../../protecting-content/implementing-the-license-server/processing-drm-requests.md#use-machine-identifiers) per informazioni su come identificare e contare i computer che fanno parte del dominio.

Se il server di dominio richiede l’autenticazione per far parte di un dominio, la richiesta deve contenere un token di autenticazione. Come per una richiesta di licenza, la registrazione del dominio può richiedere nome utente/password o l’autenticazione personalizzata.

Consulta [Autenticazione utente](../../protecting-content/implementing-the-license-server/processing-drm-requests.md#user-authentication) per informazioni dettagliate su come gestire i token di autenticazione.

Il server di dominio è responsabile dell&#39;archiviazione e della gestione delle chiavi di dominio associate a ciascun dominio. Quando è necessario generare una nuova coppia di chiavi per un dominio (la prima registrazione del dominio), è necessario richiamare `generateDomainCredential(String, int, Principal, Date)`. Questo metodo genera una nuova coppia di chiavi e un nuovo certificato di dominio. Il server di dominio deve memorizzare la chiave privata e il certificato e fornire tali oggetti durante l’elaborazione delle richieste successive per questo dominio. È inoltre possibile generare una nuova coppia di chiavi per un dominio al fine di eseguire il rollover delle chiavi. Quando passi il cursore sui tasti per un determinato dominio, accertati di incrementare la versione della chiave in `generateDomainCredential`.

Ogni volta che un computer si registra con lo stesso dominio, devono essere utilizzati la stessa chiave privata di dominio e lo stesso certificato. Richiama `addDomainCredential(DomainToken, PrivateKey)` per restituire al client una credenziale di dominio esistente. Se sono presenti più credenziali di dominio per il dominio a causa della modifica delle chiavi di dominio, il server deve fornire le credenziali di dominio per la chiave di dominio corrente e tutte le chiavi di dominio precedenti in modo che il client possa utilizzare le licenze associate a chiavi di dominio precedenti. Ciò consente di spostare una licenza associata a un vecchio token di dominio in un computer appena registrato e di continuare a essere riproducibile.
