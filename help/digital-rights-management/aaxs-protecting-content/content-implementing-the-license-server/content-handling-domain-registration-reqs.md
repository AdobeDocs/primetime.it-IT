---
title: Gestione delle richieste di registrazione del dominio
description: Gestione delle richieste di registrazione del dominio
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 0%

---


# Gestione delle richieste di registrazione del dominio{#handling-domain-registration-requests}

Se i metadati DRM indicano che la registrazione del dominio è necessaria per riprodurre il contenuto, l’applicazione client deve richiamare l’API ActionScript DRMManager.addToDeviceGroup() o l’API iOS joinLicenseDomain(). Se il client non si è ancora registrato con il server di dominio specificato (o se l’applicazione sta forzando un nuovo accesso), viene inviata una richiesta di registrazione del dominio. Il server di dominio determina se al client è consentito aggiungere un dominio ed emette una o più credenziali di dominio al client.

* La classe del gestore richieste è `com.adobe.flashaccess.sdk.protocol.domain.DomainRegistrationHandler`
* La classe del messaggio di richiesta è `com.adobe.flashaccess.sdk.protocol.domain.DomainRegistrationRequestMessage`
* Se versione 5 del protocollo di supporto client e server, l’URL della richiesta è &quot;URL del server di dominio nei metadati: + &quot;/flashaccess/domain/v4&quot;. In caso contrario, l&#39;URL della richiesta è l&#39;URL del server di dominio nei metadati &quot; + &quot;/flashaccess/domain/v3&quot;

Quando si inizializza il `DomainRegistrationHandler`, è necessario specificare l&#39;URL del server di dominio. Questo URL verrà incluso nei token di dominio emessi dal gestore per indicare il server di dominio che ha emesso il token. L’URL deve corrispondere all’URL del server di dominio specificato in qualsiasi criterio che richiede la registrazione del dominio con il server.

Per determinare se al client è consentito l’accesso al dominio, il server può esaminare le informazioni relative al computer e all’utente contenute nella richiesta. Per informazioni su come identificare e contare i computer che fanno parte del dominio, consulta [Uso degli identificatori macchina](../../aaxs-protecting-content/content-implementing-the-license-server/content-processing-aaxs-requests/content-using-machine-ids.md) . Il server può inoltre determinare a quale dominio il client è autorizzato a partecipare. Tieni presente che un client può essere solo membro di un dominio per URL del server di dominio. Se il computer dispone già di un token di dominio per questo URL del server di dominio, la richiesta di registrazione del dominio includerà il nome di dominio corrente ( `getRequestDomainName()`). Per una richiesta di ricongiungimento, il server di dominio deve restituire il set corrente di credenziali di dominio per questo dominio o restituire un errore (il server di dominio potrebbe non restituire le credenziali di dominio per un dominio diverso).

Se il server di dominio richiede l’autenticazione per l’aggiunta a un dominio, la richiesta deve contenere un token di autenticazione. Come per una richiesta di licenza, la registrazione al dominio può richiedere nome utente/password o autenticazione personalizzata. Per informazioni sulla gestione dei token di autenticazione, consulta [User authentication](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-authentication/content-user-authentication.md) .

Il server di dominio è responsabile della memorizzazione e della gestione delle chiavi di dominio associate a ciascun dominio. Quando è necessario generare una nuova coppia di chiavi per un dominio (la prima registrazione del dominio per il dominio), invoca `generateDomainCredential` `(String, int, Principal, Date)`. Questo metodo genera una nuova coppia di chiavi di dominio e un certificato di dominio. Il server di dominio deve memorizzare la chiave privata e il certificato e fornire tali oggetti durante l&#39;elaborazione delle richieste successive per questo dominio. È inoltre possibile generare una nuova coppia di chiavi per un dominio per passare il cursore sulle chiavi. Quando passi il cursore sulle chiavi di un determinato dominio, assicurati di incrementare la versione chiave anche in `generateDomainCredential`.

Ogni volta che un computer si registra con lo stesso dominio, devono essere utilizzati la stessa chiave privata e lo stesso certificato di dominio. Richiama `addDomainCredential(DomainToken, PrivateKey)` per restituire al client una credenziale di dominio esistente. Se sono presenti più credenziali di dominio per il dominio perché le chiavi di dominio sono state modificate, il server deve fornire le credenziali di dominio per la chiave di dominio corrente e tutte le chiavi di dominio precedenti in modo che il client possa utilizzare licenze associate a chiavi di dominio precedenti. Questo consente di spostare una licenza associata a un token di dominio precedente in un computer appena registrato ed essere comunque riproducibile.
