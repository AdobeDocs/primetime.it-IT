---
seo-title: Gestione delle richieste di registrazione del dominio
title: Gestione delle richieste di registrazione del dominio
uuid: e0cef9c4-b2d1-4bec-8dce-50452bc826fb
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Gestione delle richieste di registrazione del dominio{#handling-domain-registration-requests}

Se i metadati DRM indicano che per riprodurre il contenuto è necessaria la registrazione del dominio, l&#39;applicazione client deve richiamare l&#39;API ActionScript DRMManager.addToDeviceGroup() o l&#39;API iOS joinLicenseDomain(). Se il client non si è ancora registrato con il server di dominio specificato (o se l&#39;applicazione sta forzando il rientro), viene inviata una richiesta di registrazione del dominio. Il server di dominio determina se al client è consentito partecipare a un dominio ed emette una o più credenziali di dominio al client.

* La classe gestore di richieste è `com.adobe.flashaccess.sdk.protocol.domain.DomainRegistrationHandler`
* La classe del messaggio di richiesta è `com.adobe.flashaccess.sdk.protocol.domain.DomainRegistrationRequestMessage`
* Se client e server supportano entrambi il protocollo versione 5, l’URL della richiesta è &quot;URL del server di dominio nei metadati: + &quot;/flashaccess/domain/v4&quot;. In caso contrario, l’URL della richiesta è l’URL del server di dominio nei metadati &quot; + &quot;/flashaccess/domain/v3&quot;

Quando si inizializza il server `DomainRegistrationHandler`, è necessario specificare l’URL del server di dominio. Questo URL verrà incluso nei token di dominio emessi dal gestore per indicare il server di dominio che ha emesso il token. L&#39;URL deve corrispondere all&#39;URL del server di dominio specificato in qualsiasi criterio che richiede la registrazione del dominio con il server.

Per determinare se al client è consentito partecipare al dominio, il server può esaminare il computer e le informazioni utente nella richiesta. Per informazioni su come identificare e contare i computer che fanno parte del dominio, vedere [Uso degli identificatori](../../aaxs-protecting-content/content-implementing-the-license-server/content-processing-aaxs-requests/content-using-machine-ids.md) dei computer. Il server può anche determinare a quale dominio è consentito partecipare il client. Un client può essere solo un membro di un dominio per URL del server di dominio. Se il computer dispone già di un token di dominio per questo URL del server di dominio, la richiesta di registrazione del dominio includerà il nome di dominio corrente ( `getRequestDomainName()`). Per una richiesta di ricongiungimento, il server di dominio deve restituire il set corrente di credenziali di dominio per questo dominio o restituire un errore (il server di dominio potrebbe non restituire le credenziali di dominio per un dominio diverso).

Se il server di dominio richiede l&#39;autenticazione per partecipare a un dominio, la richiesta deve contenere un token di autenticazione. Come per una richiesta di licenza, la registrazione del dominio può richiedere nome utente/password o autenticazione personalizzata. Per informazioni dettagliate sulla gestione dei token di autenticazione, consultate Autenticazione [](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-authentication/content-user-authentication.md) utente.

Il server dei domini è responsabile della memorizzazione e della gestione delle chiavi di dominio associate a ciascun dominio. Quando è necessario generare una nuova coppia di chiavi per un dominio (la prima registrazione del dominio per il dominio), eseguire una chiamata `generateDomainCredential``(String, int, Principal, Date)`. Questo metodo genererà una nuova coppia di chiavi di dominio e un nuovo certificato di dominio. Il server di dominio deve memorizzare la chiave privata e il certificato e fornire tali oggetti durante l&#39;elaborazione di richieste successive per questo dominio. È inoltre possibile generare una nuova coppia di chiavi per un dominio per passare il mouse sulle chiavi. Quando si passa il puntatore del mouse sulle chiavi di un dominio specifico, assicurarsi di incrementare la versione chiave `generateDomainCredential` anche in.

Ogni volta che un computer si registra con lo stesso dominio, devono essere utilizzate la stessa chiave privata di dominio e lo stesso certificato. Richiama `addDomainCredential(DomainToken, PrivateKey)` per restituire al client una credenziale di dominio esistente. Se per il dominio sono presenti più credenziali di dominio perché le chiavi di dominio sono state modificate, il server deve fornire le credenziali di dominio per la chiave di dominio corrente e tutte le chiavi di dominio precedenti in modo che il client possa utilizzare licenze associate a chiavi di dominio precedenti. Questo consente di spostare una licenza associata a un token di dominio precedente in un computer registrato di recente e comunque riproducibile.
