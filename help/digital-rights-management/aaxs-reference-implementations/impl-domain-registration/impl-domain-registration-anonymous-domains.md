---
title: Domini anonimi
description: Domini anonimi
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---


# Domini anonimi {#anonymous-domains}

In questo caso d’uso, un numero elevato di dispositivi appartiene a un singolo dominio e l’autenticazione potrebbe non essere necessaria. Per utilizzare questo tipo di dominio con l&#39;implementazione di riferimento, crea il criterio specificando che è necessaria la registrazione del dominio. Specifica l’URL del server di dominio come `https:// host:port/flashaccess/domainserver/domainname/` e l’autenticazione anonima.

L’implementazione di riferimento implementa la seguente logica per la registrazione del dominio:

1. Analizza il nome di dominio dall’URL della richiesta.
1. Ricercare il nome di dominio nella tabella `DomainServerInfo`. Se una voce non viene trovata, inserire una voce nella tabella (valori predefiniti: l&#39;autenticazione non è necessaria e non è previsto un numero massimo di appartenenze).
1. Se è richiesta l’autenticazione per il dominio richiesto, assicurati che nella richiesta sia stato incluso un token di autenticazione valido e che corrisponda allo spazio dei nomi di autenticazione, se specificato nel database.

   1. Se l’autenticazione è obbligatoria ma non è stato fornito alcun token di autenticazione valido, restituisce l’errore `DOM_AUTHENTICATION_REQUIRED (503)`.

1. Controlla se il dispositivo si è già registrato con il dominio:

   1. Ricercare il nome di dominio nella tabella `DomainMembership`. Per ogni GUID computer trovato, confrontarlo con il GUID computer nella richiesta. Se si tratta di un nuovo computer, aggiungere una voce alla tabella `DomainMembership`.

   1. Se si tratta di un nuovo dispositivo e l&#39;appartenenza massima è già stata raggiunta, restituire l&#39;errore `DOM_LIMIT_REACHED (502)`.

1. Cerca tutte le chiavi di dominio per questo dominio nella tabella `DomainKeys`.

   1. Se `DomainServerInfo` indica che è necessario eseguire il rollover delle chiavi, genera una nuova coppia di chiavi, salvala nella tabella `DomainKeys` (con versione chiave superiore a quella esistente) e reimposta il flag `Key Rollover Required` in `DomainServerInfo`.

   1. Per ogni chiave di dominio, genera una credenziale di dominio.

L’implementazione di riferimento implementa la seguente logica per la deregistrazione del dominio:

1. Analizza il nome di dominio dall’URL della richiesta.
1. Ricercare il nome di dominio richiesto nella tabella `DomainServerInfo`.
1. Se è richiesta l’autenticazione per il dominio richiesto, assicurati che nella richiesta sia stato incluso un token di autenticazione valido e che corrisponda allo spazio dei nomi di autenticazione, se specificato nel database.
1. Ricercare il nome di dominio e il GUID del computer nella tabella `DomainMembership`. Se non viene trovata una voce corrispondente, restituisce l&#39;errore `DEREG_DENIED (401)`.

1. Se non si tratta di una richiesta di anteprima, elimina la voce da `DomainMembership` e imposta il flag `Key Rollover Required` in `DomainServerInfo`.

In questo caso d’uso, poiché un numero elevato di computer potrebbe entrare a far parte del dominio, non è possibile stabilire una corrispondenza completa dell’ID computer. Viene invece utilizzato il GUID della macchina casuale assegnato al computer durante l&#39;individualizzazione.
