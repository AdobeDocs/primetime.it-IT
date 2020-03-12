---
seo-title: Domini anonimi
title: Domini anonimi
uuid: ee29ae4d-65b2-48de-b441-18c8cf55de32
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Domini anonimi {#anonymous-domains}

In questo caso, un numero elevato di dispositivi appartiene a un solo dominio e l&#39;autenticazione potrebbe non essere necessaria. Per utilizzare questo tipo di dominio con l&#39;implementazione del riferimento, creare il criterio specificando che è necessaria la registrazione del dominio. Specificate l&#39;URL del server di dominio come [*!DNL https:// host:port/flashaccess/domainserver/domainname/*] e l&#39;autenticazione anonima.

L&#39;implementazione di riferimento implementa la seguente logica per la registrazione del dominio:

1. Analizzate il nome del dominio dall’URL della richiesta.
1. Cerca il nome del dominio nella `DomainServerInfo` tabella. Se una voce non viene trovata, inserire una voce nella tabella (valori predefiniti: l&#39;autenticazione non è obbligatoria e non è previsto alcun numero massimo di appartenenze).
1. Se l&#39;autenticazione è necessaria per il dominio richiesto, accertatevi che nella richiesta sia stato incluso un token di autenticazione valido e che corrisponda allo spazio dei nomi di autenticazione, se specificato nel database.

   1. Se l&#39;autenticazione è obbligatoria ma non è stato fornito alcun token di autenticazione valido, restituisce un errore `DOM_AUTHENTICATION_REQUIRED (503)`.

1. Verificate che il dispositivo si sia già registrato con il dominio:

   1. Cerca il nome del dominio nella `DomainMembership` tabella. Per ciascun GUID computer trovato, confrontate con il GUID computer nella richiesta. Se si tratta di un nuovo computer, aggiungere una voce alla `DomainMembership` tabella.

   1. Se si tratta di un nuovo dispositivo e è già stato raggiunto il limite massimo di appartenenza, restituisce un errore `DOM_LIMIT_REACHED (502)`.

1. Cerca tutte le chiavi di dominio per questo dominio nella `DomainKeys` tabella.

   1. Se `DomainServerInfo` indica che è necessario scorrere i tasti, generare una nuova coppia di chiavi, salvarla nella `DomainKeys` tabella (con la versione chiave 1 superiore alla chiave esistente più alta) e reimpostare il `Key Rollover Required` flag in `DomainServerInfo`.

   1. Per ogni chiave di dominio, genera una credenziale di dominio.

L&#39;implementazione di riferimento implementa la seguente logica per la deregistrazione del dominio:

1. Analizzate il nome del dominio dall’URL della richiesta.
1. Cerca il nome di dominio richiesto nella `DomainServerInfo` tabella.
1. Se l&#39;autenticazione è necessaria per il dominio richiesto, accertatevi che nella richiesta sia stato incluso un token di autenticazione valido e che corrisponda allo spazio dei nomi di autenticazione, se specificato nel database.
1. Cerca il nome di dominio e il GUID del computer nella `DomainMembership` tabella. Se non viene trovata una voce corrispondente, restituisce un errore `DEREG_DENIED (401)`.

1. Se non si tratta di una richiesta di anteprima, eliminate la voce `DomainMembership` e impostate il `Key Rollover Required` flag in `DomainServerInfo`.

In questo caso d’uso, poiché un numero elevato di computer poteva accedere al dominio, non è possibile stabilire una corrispondenza completa con l’ID del computer. Viene invece utilizzato il GUID del computer casuale assegnato al computer durante l&#39;individualizzazione.
