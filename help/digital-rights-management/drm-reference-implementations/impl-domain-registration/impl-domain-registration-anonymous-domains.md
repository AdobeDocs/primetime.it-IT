---
description: 'null'
seo-description: 'null'
seo-title: Logica dominio anonima
title: Logica dominio anonima
uuid: bd0e8e51-27dc-4ccf-b285-a80c2ab9e260
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Logica dominio anonima{#anonymous-domain-logic}

## Logica di registrazione del dominio {#section_C91DCD49D7D44570AF98C2D7B8A283F9}

L’implementazione di riferimento applica la seguente logica per la registrazione del dominio anonimo:

1. Analizzate il nome del dominio dall’URL della richiesta.
1. Cerca il nome del dominio nella `DomainServerInfo` tabella.
1. Se non è possibile individuare una voce, inserire una voce nella tabella.

   I valori predefiniti sono:

   * `authentication is not required`
   * `no membership maximum`
   Se per il dominio richiesto è necessaria l&#39;autenticazione, verificate che nella richiesta sia presente un token di autenticazione valido. Se nel database è specificato Auth Namespace, il token deve corrispondere allo spazio dei nomi di autenticazione specificato.
1. Se l&#39;autenticazione è obbligatoria, ma non è disponibile un token di autenticazione valido, restituisce un errore `DOM_AUTHENTICATION_REQUIRED (503)`.
1. Verificate che il dispositivo sia registrato nel dominio:

   1. Cerca il nome del dominio nella `DomainMembership` tabella.
   1. Confrontare il GUID del computer che si trova con il GUID del computer nella richiesta.
   1. Se si tratta di un nuovo computer, aggiungere una voce nella `DomainMembership` tabella.
   1. Se è stato raggiunto un nuovo dispositivo e `Max Membership` un valore, restituisce un errore `DOM_LIMIT_REACHED (502)`.

1. Cerca tutte le chiavi di dominio per questo dominio nella `DomainKeys` tabella:

   1. Se `DomainServerInfo` indica che è necessario scorrere i tasti, generare una nuova coppia di chiavi.
   1. Salvare la coppia di chiavi nella `DomainKeys` tabella, con una versione chiave che è un numero superiore alla chiave più alta esistente.
   1. Reimpostare il `Key Rollover Required` flag in `DomainServerInfo`.

   1. Per ogni chiave di dominio, genera una credenziale di dominio.

## Logica di deregistrazione del dominio {#section_C968BBFCBFAB4510A903D169F38C9FCE}

L&#39;implementazione di riferimento applica la seguente logica per la deregistrazione del dominio anonimo:

1. Analizzate il nome del dominio dall’URL della richiesta.
1. Cerca il nome di dominio richiesto nella `DomainServerInfo` tabella.
1. Se per il dominio richiesto è necessaria l&#39;autenticazione, verificate che nella richiesta sia presente un token di autenticazione valido.

   Il token deve anche corrispondere allo spazio dei nomi di autenticazione specificato nel database.
1. Cercare il nome di dominio e il GUID del computer nella `DomainMembership` tabella.

   Se non è possibile individuare una voce corrispondente, restituisce un errore `DEREG_DENIED (401)`.

1. Se non si tratta di una richiesta di anteprima, eliminate la voce da `DomainMembership`e in `DomainServerInfo`, impostate il `Key Rollover Required` flag.

Poiché un numero elevato di computer potrebbe entrare a far parte del dominio, non è possibile corrispondere semplicemente all&#39;ID computer. Viene invece applicato il GUID del computer casuale assegnato al computer durante l&#39;individualizzazione.
