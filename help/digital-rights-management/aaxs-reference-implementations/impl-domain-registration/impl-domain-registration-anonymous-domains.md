---
seo-title: Domini anonimi
title: Domini anonimi
uuid: ee29ae4d-65b2-48de-b441-18c8cf55de32
translation-type: tm+mt
source-git-commit: 4f196bbd079edeb1a423afee6b4b7e249d380f40
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---


# Domini anonimi {#anonymous-domains}

In questo caso, un numero elevato di dispositivi appartiene a un solo dominio e l&#39;autenticazione potrebbe non essere necessaria. Per utilizzare questo tipo di dominio con l&#39;implementazione del riferimento, creare il criterio specificando che è necessaria la registrazione del dominio. Specificate l&#39;URL del server di dominio come `https:// host:port/flashaccess/domainserver/domainname/` e specificate l&#39;autenticazione anonima.

L&#39;implementazione di riferimento implementa la seguente logica per la registrazione del dominio:

1. Analizzate il nome del dominio dall’URL della richiesta.
1. Cerca il nome del dominio nella tabella `DomainServerInfo`. Se una voce non viene trovata, inserire una voce nella tabella (valori predefiniti: l&#39;autenticazione non è obbligatoria e non è previsto alcun numero massimo di appartenenze).
1. Se l&#39;autenticazione è necessaria per il dominio richiesto, accertatevi che nella richiesta sia stato incluso un token di autenticazione valido e che corrisponda allo spazio dei nomi di autenticazione, se specificato nel database.

   1. Se l&#39;autenticazione è obbligatoria ma non è stato fornito alcun token di autenticazione valido, restituisci l&#39;errore `DOM_AUTHENTICATION_REQUIRED (503)`.

1. Verificate che il dispositivo si sia già registrato con il dominio:

   1. Cerca il nome del dominio nella tabella `DomainMembership`. Per ciascun GUID computer trovato, confrontate con il GUID computer nella richiesta. Se si tratta di un nuovo computer, aggiungere una voce alla tabella `DomainMembership`.

   1. Se si tratta di un nuovo dispositivo e è già stato raggiunto il limite massimo di appartenenza, restituite l&#39;errore `DOM_LIMIT_REACHED (502)`.

1. Cerca tutte le chiavi di dominio per questo dominio nella tabella `DomainKeys`.

   1. Se `DomainServerInfo` indica che è necessario scorrere i tasti, generare una nuova coppia di chiavi, salvarla nella tabella `DomainKeys` (con una versione chiave superiore alla chiave più alta esistente) e reimpostare il flag `Key Rollover Required` in `DomainServerInfo`.

   1. Per ogni chiave di dominio, genera una credenziale di dominio.

L&#39;implementazione di riferimento implementa la seguente logica per la deregistrazione del dominio:

1. Analizzate il nome del dominio dall’URL della richiesta.
1. Cerca il nome di dominio richiesto nella tabella `DomainServerInfo`.
1. Se l&#39;autenticazione è necessaria per il dominio richiesto, accertatevi che nella richiesta sia stato incluso un token di autenticazione valido e che corrisponda allo spazio dei nomi di autenticazione, se specificato nel database.
1. Cerca il nome di dominio e il GUID del computer nella tabella `DomainMembership`. Se non viene trovata una voce corrispondente, restituisce l&#39;errore `DEREG_DENIED (401)`.

1. Se non si tratta di una richiesta di anteprima, eliminare la voce da `DomainMembership` e impostare il flag `Key Rollover Required` in `DomainServerInfo`.

In questo caso d’uso, poiché un numero elevato di computer poteva accedere al dominio, non è possibile stabilire una corrispondenza completa con l’ID del computer. Viene invece utilizzato il GUID del computer casuale assegnato al computer durante l&#39;individualizzazione.
