---
title: Domini anonimi
description: Domini anonimi
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---

# Domini anonimi {#anonymous-domains}

In questo caso d’uso, un numero elevato di dispositivi appartiene a un singolo dominio e l’autenticazione potrebbe non essere necessaria. Per utilizzare questo tipo di dominio con l’implementazione di riferimento, crea il criterio specificando che è necessaria la registrazione del dominio. Specifica l’URL del server di dominio come `https:// host:port/flashaccess/domainserver/domainname/` e specifica l’autenticazione anonima.

L’implementazione di riferimento implementa la seguente logica per la registrazione del dominio:

1. Analizza il nome di dominio dall’URL della richiesta.
1. Ricercare il nome di dominio in `DomainServerInfo` tabella. Se non viene trovata alcuna voce, inserire una voce nella tabella (valori predefiniti: autenticazione non richiesta e nessuna appartenenza massima).
1. Se è richiesta l’autenticazione per il dominio richiesto, accertati che nella richiesta sia stato incluso un token di autenticazione valido e che corrisponda allo spazio dei nomi di autenticazione, se specificato nel database.

   1. Se è richiesta l’autenticazione ma non è stato fornito alcun token di autenticazione valido, viene restituito un errore `DOM_AUTHENTICATION_REQUIRED (503)`.

1. Verifica se il dispositivo è già stato registrato con il dominio:

   1. Ricercare il nome di dominio in `DomainMembership` tabella. Per ogni GUID di computer trovato, confrontare con il GUID di computer nella richiesta. Se si tratta di un nuovo computer, aggiungere una voce al `DomainMembership` tabella.

   1. Se si tratta di un nuovo dispositivo e è già stato raggiunto il numero massimo di iscritti, viene restituito un errore `DOM_LIMIT_REACHED (502)`.

1. Cerca tutte le chiavi di dominio per questo dominio in `DomainKeys` tabella.

   1. Se `DomainServerInfo` indica che è necessario eseguire il rollover delle chiavi, generare una nuova coppia di chiavi e salvarla in `DomainKeys` (con la versione della chiave 1 superiore alla chiave esistente più elevata) e reimposta la `Key Rollover Required` contrassegna in `DomainServerInfo`.

   1. Per ogni chiave di dominio, genera una credenziale di dominio.

L’implementazione di riferimento implementa la seguente logica per la de-registrazione del dominio:

1. Analizza il nome di dominio dall’URL della richiesta.
1. Ricercare il nome di dominio richiesto in `DomainServerInfo` tabella.
1. Se è richiesta l’autenticazione per il dominio richiesto, accertati che nella richiesta sia stato incluso un token di autenticazione valido e che corrisponda allo spazio dei nomi di autenticazione, se specificato nel database.
1. Ricercare il nome di dominio e il GUID del computer in `DomainMembership` tabella. Se non viene trovata una voce corrispondente, viene restituito un errore `DEREG_DENIED (401)`.

1. Se non si tratta di una richiesta di anteprima, elimina la voce da `DomainMembership` e imposta `Key Rollover Required` contrassegna in `DomainServerInfo`.

In questo caso d’uso, poiché un numero elevato di computer potrebbe far parte del dominio, non è possibile trovare una corrispondenza completa con l’ID computer. Viene invece utilizzato il GUID casuale del computer assegnato al computer durante l&#39;individualizzazione.
