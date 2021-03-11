---
title: Logica del dominio anonimo
description: Logica del dominio anonimo
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---


# Logica del dominio anonimo{#anonymous-domain-logic}

## Logica di registrazione del dominio {#section_C91DCD49D7D44570AF98C2D7B8A283F9}

L’implementazione di riferimento applica la seguente logica per la registrazione del dominio anonimo:

1. Analizza il nome di dominio dall’URL della richiesta.
1. Cerca il nome di dominio nella tabella `DomainServerInfo`.
1. Se non è possibile individuare una voce, inserire una voce nella tabella.

   I valori predefiniti sono:

   * `authentication is not required`
   * `no membership maximum`

   Se è richiesta l’autenticazione per il dominio richiesto, assicurati che nella richiesta sia presente un token di autenticazione valido. Se nel database è specificato lo spazio dei nomi di autenticazione, il token deve corrispondere allo spazio dei nomi di autenticazione specificato.
1. Se è richiesta l’autenticazione, ma non è disponibile un token di autenticazione valido, restituisce l’errore `DOM_AUTHENTICATION_REQUIRED (503)`.
1. Controlla se il dispositivo è registrato con il dominio:

   1. Cerca il nome di dominio nella tabella `DomainMembership`.
   1. Confrontare il GUID del computer individuato con il GUID del computer nella richiesta.
   1. Se si tratta di un nuovo computer, aggiungere una voce nella tabella `DomainMembership`.
   1. Se si tratta di un nuovo dispositivo e il valore `Max Membership` è stato raggiunto, restituisce l&#39;errore `DOM_LIMIT_REACHED (502)`.

1. Cerca tutte le chiavi di dominio per questo dominio nella tabella `DomainKeys`:

   1. Se `DomainServerInfo` indica che è necessario eseguire il rollover delle chiavi, genera una nuova coppia di chiavi.
   1. Salvare la coppia di chiavi nella tabella `DomainKeys`, con una versione chiave che è un numero superiore alla chiave esistente più alta.
   1. Reimposta il flag `Key Rollover Required` in `DomainServerInfo`.

   1. Per ogni chiave di dominio, genera una credenziale di dominio.

## Logica di cancellazione del dominio {#section_C968BBFCBFAB4510A903D169F38C9FCE}

L&#39;implementazione di riferimento applica la seguente logica per la deregistrazione del dominio anonimo:

1. Analizza il nome di dominio dall’URL della richiesta.
1. Cerca il nome di dominio richiesto nella tabella `DomainServerInfo`.
1. Se è richiesta l’autenticazione per il dominio richiesto, assicurati che nella richiesta sia presente un token di autenticazione valido.

   Il token deve anche corrispondere allo spazio dei nomi di autenticazione specificato nel database.
1. Cerca il nome di dominio e il GUID del computer nella tabella `DomainMembership`.

   Se non è possibile individuare una voce corrispondente, restituire l&#39;errore `DEREG_DENIED (401)`.

1. Se non si tratta di una richiesta di anteprima, elimina la voce da `DomainMembership` e in `DomainServerInfo` imposta il flag `Key Rollover Required`.

Poiché un numero elevato di computer può entrare a far parte del dominio, non è possibile abbinare semplicemente l&#39;ID computer. Viene invece applicato il GUID della macchina casuale assegnato al computer durante l&#39;individualizzazione.
