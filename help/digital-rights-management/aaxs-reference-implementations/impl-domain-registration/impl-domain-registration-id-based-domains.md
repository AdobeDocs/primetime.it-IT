---
seo-title: Domini basati su identità
title: Domini basati su identità
uuid: 34cad19b-1adb-4e0c-ac59-50632f6988f7
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Domini basati su identità {#identity-based-domains}

In questo caso d’uso, ogni utente autenticato ha un proprio dominio, e un certo numero di dispositivi può accedere al dominio. Per utilizzare questo tipo di dominio con l&#39;implementazione del riferimento, è necessario creare un criterio che specifichi la registrazione del dominio. Specificate l&#39;host e la porta del server per l&#39;URL del server di dominio e l&#39;autenticazione nome utente/password è obbligatoria.

L&#39;implementazione di riferimento implementa la seguente logica per la registrazione del dominio:

1. Determinare il nome di dominio da assegnare a questo utente. Il nome di dominio sarà * `namequalifier:username`* estratto dal token di autenticazione. Se non è presente un token di autenticazione, restituite l&#39;errore DOM_AUTHENTICATION_REQUIRED (503).
1. Cerca il nome del dominio nella `DomainServerInfo` tabella. Se una voce non viene trovata, inserire una voce nella tabella (i valori predefiniti sono l&#39;autenticazione obbligatoria, appartenenza al dominio max=5).
1. Verificate che il dispositivo si sia già registrato con il dominio:

   1. Cerca il nome del dominio nella `UserDomainMembership` tabella. Per ciascun ID computer trovato, confrontate con l&#39;ID computer nella richiesta. Se si tratta di un nuovo computer, aggiungere una voce alla `UserDomainMembership` tabella. Quindi, trova i record corrispondenti nella `UserDomainRefCount` tabella. Se non esiste una voce per il GUID del computer, aggiungere un record.

   1. Se si tratta di un nuovo dispositivo e è già stato raggiunto il limite massimo di appartenenza, restituite l&#39;errore DOM_LIMIT_REACHED (502).

1. Cerca tutte le chiavi di dominio per questo dominio nella tabella DomainKeys.

   1. Se `DomainServerInfo` indica che è necessario scorrere i tasti, generate una nuova coppia di chiavi, salvatela nella `DomainKeys` tabella (con la versione del tasto superiore di 1 rispetto alla chiave esistente più alta) e reimpostate il flag &quot;Rollover chiave necessaria&quot; in `DomainServerInfo`.

   1. Per ogni chiave di dominio, genera una credenziale di dominio.

L’implementazione di riferimento implementa la seguente logica per la deregistrazione del dominio:

1. Determinare il nome di dominio da assegnare a questo utente. Il nome di dominio sarà *nomequalifier:nomeutente* estratto dal token di autenticazione. Se non è presente un token di autenticazione, restituite l&#39;errore DOM_AUTHENTICATION_REQUIRED (503).
1. Cerca il nome di dominio richiesto nella `DomainServerInfo` tabella.
1. Cerca il nome del dominio nella `UserDomainMembership` tabella. Per ciascun ID computer trovato, confrontate con l&#39;ID computer nella richiesta. Trovare la voce corrispondente nella `UserDomainRefCount` tabella. Se non viene trovata una voce corrispondente, restituire l&#39;errore DEREG_DENIED (401).

1. Se non si tratta di una richiesta di anteprima, eliminate la voce dalla `UserDomainRefCount` tabella. Se la tabella non contiene più voci per il computer, eliminare la voce `UserDomainMembership` e impostare il flag &quot;Rollover necessario chiave&quot; in `DomainServerInfo`.

In questo caso d&#39;uso, ogni utente può registrare un numero limitato di computer, in modo da poter utilizzare l&#39;ID computer completo e il `matches()` metodo per contare accuratamente i computer. Tuttavia, poiché l&#39;utente può registrarsi più volte su questo computer (attraverso più applicazioni AIR o lettori in browser diversi), anche il server deve mantenere un numero di riferimento, in modo che la cancellazione della registrazione possa essere conteggiata accuratamente. La deregistrazione non può essere considerata completa, finché non vengono restituiti tutti i token di dominio presenti nel computer.
