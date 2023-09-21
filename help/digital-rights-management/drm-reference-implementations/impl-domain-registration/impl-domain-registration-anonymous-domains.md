---
title: Logica di dominio anonimo
description: Logica di dominio anonimo
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---

# Logica di dominio anonimo{#anonymous-domain-logic}

## Logica di registrazione del dominio {#section_C91DCD49D7D44570AF98C2D7B8A283F9}

L’implementazione di riferimento applica la seguente logica per la registrazione del dominio anonimo:

1. Analizza il nome di dominio dall’URL della richiesta.
1. Cercare il nome di dominio in `DomainServerInfo` tabella.
1. Se non è possibile individuare una voce, inserire una voce nella tabella.

   I valori predefiniti sono:

   * `authentication is not required`
   * `no membership maximum`

   Se è richiesta l’autenticazione per il dominio richiesto, accertati che nella richiesta sia presente un token di autenticazione valido. Se lo spazio dei nomi di autenticazione è specificato nel database, il token deve corrispondere allo spazio dei nomi di autenticazione specificato.
1. Se è richiesta l’autenticazione ma non è disponibile un token di autenticazione valido, viene restituito un errore `DOM_AUTHENTICATION_REQUIRED (503)`.
1. Verifica se il dispositivo è registrato con il dominio:

   1. Cercare il nome di dominio in `DomainMembership` tabella.
   1. Confrontare il GUID del computer individuato con il GUID del computer nella richiesta.
   1. Se si tratta di un nuovo computer, aggiungere una voce nella `DomainMembership` tabella.
   1. Se si tratta di un nuovo dispositivo e `Max Membership` è stato raggiunto il valore, viene restituito un errore `DOM_LIMIT_REACHED (502)`.

1. Cerca tutte le chiavi di dominio per questo dominio nel `DomainKeys` tabella:

   1. Se `DomainServerInfo` indica che è necessario eseguire il rollover delle chiavi e generare una nuova coppia di chiavi.
   1. Salva la coppia di chiavi in `DomainKeys` con una versione di chiave superiore di un numero rispetto alla chiave esistente più elevata.
   1. Reimposta `Key Rollover Required` contrassegna in `DomainServerInfo`.

   1. Per ogni chiave di dominio, genera una credenziale di dominio.

## Logica di annullamento registrazione dominio {#section_C968BBFCBFAB4510A903D169F38C9FCE}

L’implementazione di riferimento applica la seguente logica per la de-registrazione del dominio anonimo:

1. Analizza il nome di dominio dall’URL della richiesta.
1. Cercare il nome di dominio richiesto in `DomainServerInfo` tabella.
1. Se è richiesta l’autenticazione per il dominio richiesto, accertati che nella richiesta sia presente un token di autenticazione valido.

   Il token deve inoltre corrispondere allo spazio dei nomi di autenticazione specificato nel database.
1. Cercare il nome di dominio e il GUID del computer in `DomainMembership` tabella.

   Se non riesci a individuare una voce corrispondente, restituisce un errore `DEREG_DENIED (401)`.

1. Se non si tratta di una richiesta di anteprima, elimina la voce da `DomainMembership`, e in `DomainServerInfo`, imposta `Key Rollover Required` flag.

Poiché un numero elevato di computer può far parte del dominio, non è sufficiente che l&#39;ID computer corrisponda. Viene invece applicato il GUID casuale del computer assegnato al computer durante la personalizzazione.
