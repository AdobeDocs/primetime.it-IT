---
seo-title: Gestione delle richieste di registrazione del dominio
title: Gestione delle richieste di registrazione del dominio
uuid: d92db6c2-5a16-41ea-a1aa-541c59780678
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

---


# Gestione delle richieste di registrazione del dominio {#handle-domain-registration-requests}

Se i metadati DRM indicano che per riprodurre il contenuto è necessaria la registrazione del dominio, l&#39;applicazione client deve richiamare l&#39;API `DRMManager.addToDeviceGroup()` ActionScript o l&#39;API `joinLicenseDomain()` iOS. Se il client non si è ancora registrato con il server di dominio specificato (o se l&#39;applicazione sta forzando il rientro), viene inviata una richiesta di registrazione del dominio. Il server di dominio determina se al client è consentito partecipare a un dominio ed emette una o più credenziali di dominio al client.

* La classe gestore di richieste è `com.adobe.flashaccess.sdk.protocol.domain.DomainRegistrationHandler`
* La classe del messaggio di richiesta è `com.adobe.flashaccess.sdk.protocol.domain.DomainRegistrationRequestMessage`
* Se client e server supportano entrambi il protocollo versione 5, l’URL della richiesta è &quot;URL del server di dominio nei metadati: + &quot; [!DNL /flashaccess/domain/v4]&quot;. In caso contrario, l’URL della richiesta è l’URL del server di dominio nei metadati &quot; + &quot; [!DNL /flashaccess/domain/v3]&quot;

Quando inizializzate l&#39;URL `DomainRegistrationHandler`, dovete specificare l&#39;URL del server di dominio. Questo URL viene quindi incluso nei token di dominio emessi dal gestore per indicare al server di dominio che il token è stato emesso. L&#39;URL deve corrispondere all&#39;URL del server di dominio specificato in qualsiasi criterio DRM che richiede la registrazione del dominio con il server.

Per determinare se al client è consentito partecipare al dominio, il server può esaminare il computer e le informazioni utente nella richiesta. Il server può anche determinare a quale dominio è consentito partecipare il client.

>[!NOTE]
>
>Un client può essere solo un membro di un dominio per URL del server di dominio. Se il computer dispone già di un token di dominio per questo URL del server di dominio, la richiesta di registrazione del dominio include il nome di dominio corrente ( `getRequestDomainName()`).

Per una richiesta di ricongiungimento, il server di dominio deve restituire il set corrente di credenziali di dominio per questo dominio o restituire un errore. Il server del dominio potrebbe non restituire le credenziali del dominio per un dominio diverso.

Per informazioni su come identificare e contare i computer che fanno parte del dominio, vedere [Uso degli identificatori](../../protecting-content/implementing-the-license-server/processing-drm-requests.md#use-machine-identifiers) dei computer.

Se il server di dominio richiede l&#39;autenticazione per partecipare a un dominio, la richiesta deve contenere un token di autenticazione. Come per una richiesta di licenza, la registrazione del dominio può richiedere nome utente/password o autenticazione personalizzata.

Per informazioni dettagliate sulla gestione dei token di autenticazione, consultate Autenticazione [](../../protecting-content/implementing-the-license-server/processing-drm-requests.md#user-authentication) utente.

Il server dei domini è responsabile della memorizzazione e della gestione delle chiavi di dominio associate a ciascun dominio. Quando è necessario generare una nuova coppia di chiavi per un dominio (la prima registrazione del dominio per il dominio), è necessario richiamare `generateDomainCredential(String, int, Principal, Date)`. Questo metodo genera una nuova coppia di chiavi di dominio e un nuovo certificato di dominio. Il server di dominio deve memorizzare la chiave privata e il certificato e fornire tali oggetti durante l&#39;elaborazione di richieste successive per questo dominio. È inoltre possibile generare una nuova coppia di chiavi per un dominio per passare il mouse sulle chiavi. Quando passi il cursore sulle chiavi di un dominio specifico, assicurati di incrementare la versione chiave in `generateDomainCredential`.

Ogni volta che un computer si registra con lo stesso dominio, devono essere utilizzate la stessa chiave privata di dominio e lo stesso certificato. Richiama `addDomainCredential(DomainToken, PrivateKey)` per restituire al client una credenziale di dominio esistente. Se per il dominio sono presenti più credenziali di dominio perché le chiavi di dominio sono state modificate, il server deve fornire le credenziali di dominio per la chiave di dominio corrente e tutte le chiavi di dominio precedenti in modo che il client possa utilizzare licenze associate a chiavi di dominio precedenti. Questo consente di spostare una licenza associata a un token di dominio precedente in un computer registrato di recente e comunque riproducibile.
