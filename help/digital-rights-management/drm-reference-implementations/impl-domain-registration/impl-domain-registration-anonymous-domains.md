---
description: 'null'
seo-description: 'null'
seo-title: Logica dominio anonima
title: Logica dominio anonima
uuid: bd0e8e51-27dc-4ccf-b285-a80c2ab9e260
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---


# Logica dominio anonima{#anonymous-domain-logic}

## Logica di registrazione del dominio {#section_C91DCD49D7D44570AF98C2D7B8A283F9}

L’implementazione di riferimento applica la seguente logica per la registrazione del dominio anonimo:

1. Analizzate il nome del dominio dall’URL della richiesta.
1. Cerca il nome del dominio nella tabella `DomainServerInfo`.
1. Se non è possibile individuare una voce, inserire una voce nella tabella.

   I valori predefiniti sono:

   * `authentication is not required`
   * `no membership maximum`

   Se per il dominio richiesto è necessaria l&#39;autenticazione, verificate che nella richiesta sia presente un token di autenticazione valido. Se nel database è specificato Auth Namespace, il token deve corrispondere allo spazio dei nomi di autenticazione specificato.
1. Se l&#39;autenticazione è obbligatoria, ma non è disponibile un token di autenticazione valido, restituire l&#39;errore `DOM_AUTHENTICATION_REQUIRED (503)`.
1. Verificate che il dispositivo sia registrato nel dominio:

   1. Cerca il nome del dominio nella tabella `DomainMembership`.
   1. Confrontare il GUID del computer che si trova con il GUID del computer nella richiesta.
   1. Se si tratta di un nuovo computer, aggiungere una voce nella tabella `DomainMembership`.
   1. Se si tratta di un nuovo dispositivo e il valore `Max Membership` è stato raggiunto, restituire l&#39;errore `DOM_LIMIT_REACHED (502)`.

1. Cerca tutte le chiavi di dominio per questo dominio nella tabella `DomainKeys`:

   1. Se `DomainServerInfo` indica che è necessario scorrere i tasti, generare una nuova coppia di chiavi.
   1. Salvare la coppia di chiavi nella tabella `DomainKeys`, con una versione chiave che è un numero superiore alla chiave più alta esistente.
   1. Reimpostare il flag `Key Rollover Required` in `DomainServerInfo`.

   1. Per ogni chiave di dominio, genera una credenziale di dominio.

## Logica di deregistrazione del dominio {#section_C968BBFCBFAB4510A903D169F38C9FCE}

L&#39;implementazione di riferimento applica la seguente logica per la deregistrazione del dominio anonimo:

1. Analizzate il nome del dominio dall’URL della richiesta.
1. Cerca il nome di dominio richiesto nella tabella `DomainServerInfo`.
1. Se per il dominio richiesto è necessaria l&#39;autenticazione, verificate che nella richiesta sia presente un token di autenticazione valido.

   Il token deve anche corrispondere allo spazio dei nomi di autenticazione specificato nel database.
1. Cercare il nome di dominio e il GUID del computer nella tabella `DomainMembership`.

   Se non riuscite a individuare una voce corrispondente, restituite l&#39;errore `DEREG_DENIED (401)`.

1. Se non si tratta di una richiesta di anteprima, eliminare la voce da `DomainMembership` e impostare il flag `DomainServerInfo` in `Key Rollover Required`.

Poiché un numero elevato di computer potrebbe entrare a far parte del dominio, non è possibile corrispondere semplicemente all&#39;ID computer. Viene invece applicato il GUID del computer casuale assegnato al computer durante l&#39;individualizzazione.
