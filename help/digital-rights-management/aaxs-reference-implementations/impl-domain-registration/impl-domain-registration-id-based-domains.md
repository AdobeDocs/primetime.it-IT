---
title: Domini basati su identità
description: Domini basati su identità
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---


# Domini basati su identità {#identity-based-domains}

In questo caso d’uso, ogni utente autenticato dispone di un proprio dominio e un certo numero di dispositivi può accedere al dominio. Per utilizzare questo tipo di dominio con l&#39;implementazione di riferimento, crea un criterio che specifichi la registrazione del dominio obbligatoria. Specifica l&#39;host e la porta del server per l&#39;URL del server di dominio e specifica che è richiesta l&#39;autenticazione con nome utente e password.

L’implementazione di riferimento implementa la seguente logica per la registrazione del dominio:

1. Determinare il nome di dominio da assegnare a questo utente. Il nome di dominio sarà * `namequalifier:username`* estratto dal token di autenticazione. Se non è presente alcun token di autenticazione, restituisce l’errore DOM_AUTHENTICATION_REQUIRED (503).
1. Ricercare il nome di dominio nella tabella `DomainServerInfo`. Se non viene trovata una voce, inserisci una voce nella tabella (i valori predefiniti sono autenticazione obbligatoria, appartenenza al dominio max=5).
1. Controlla se il dispositivo si è già registrato con il dominio:

   1. Cerca il nome di dominio nella tabella `UserDomainMembership`. Per ogni ID computer trovato, confronta con l&#39;ID computer nella richiesta. Se si tratta di un nuovo computer, aggiungere una voce alla tabella `UserDomainMembership`. Quindi, trova i record corrispondenti nella tabella `UserDomainRefCount`. Se non esiste una voce per questo GUID computer, aggiungere un record.

   1. Se si tratta di un nuovo dispositivo e l&#39;appartenenza massima è già stata raggiunta, restituire l&#39;errore DOM_LIMIT_REACHED (502).

1. Ricercare tutte le chiavi di dominio per questo dominio nella tabella DomainKeys.

   1. Se `DomainServerInfo` indica che è necessario eseguire il rollover dei tasti, genera una nuova coppia di chiavi, salvala nella tabella `DomainKeys` (con versione chiave superiore a quella esistente) e reimposta il flag &quot;Key Rollover Required&quot; in `DomainServerInfo`.

   1. Per ogni chiave di dominio, genera una credenziale di dominio.

L’implementazione di riferimento implementa la seguente logica per la deregistrazione del dominio:

1. Determinare il nome di dominio da assegnare a questo utente. Il nome di dominio sarà *nomequalifier:username* estratto dal token di autenticazione. Se non è presente alcun token di autenticazione, restituisce l’errore DOM_AUTHENTICATION_REQUIRED (503).
1. Ricercare il nome di dominio richiesto nella tabella `DomainServerInfo`.
1. Ricercare il nome di dominio nella tabella `UserDomainMembership`. Per ogni ID computer trovato, confronta con l&#39;ID computer nella richiesta. Trova la voce corrispondente nella tabella `UserDomainRefCount`. Se non viene trovata una voce corrispondente, restituire l&#39;errore DEREG_DENIED (401).

1. Se non si tratta di una richiesta di anteprima, elimina la voce dalla tabella `UserDomainRefCount`. Se la macchina non contiene più voci, eliminare la voce da `UserDomainMembership` e impostare il flag &quot;Key Rollover Required&quot; in `DomainServerInfo`.

In questo caso d&#39;uso, ogni utente può registrare un numero limitato di computer, in modo da poter utilizzare l&#39;ID macchina completo e il metodo `matches()` per contare accuratamente i computer. Tuttavia, poiché l&#39;utente può registrarsi più volte su questa macchina (attraverso più applicazioni AIR o lettori in diversi browser), il server deve anche mantenere un conteggio di riferimento, in modo che la cancellazione della registrazione possa essere conteggiata con precisione. La deregistrazione non può essere considerata completa finché non vengono consegnati tutti i token di dominio sul computer.
