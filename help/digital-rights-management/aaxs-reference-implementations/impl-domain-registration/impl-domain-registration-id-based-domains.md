---
title: Domini basati su identità
description: Domini basati su identità
copied-description: true
exl-id: de7b6c8a-5227-4679-933a-3278921903d7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---

# Domini basati su identità {#identity-based-domains}

In questo caso d’uso, ogni utente autenticato ha il proprio dominio e un determinato numero di dispositivi può essere aggiunto al dominio. Per utilizzare questo tipo di dominio con l’implementazione di riferimento, è necessario creare un criterio che specifichi la registrazione del dominio. Specificare l&#39;host e la porta del server per l&#39;URL del server di dominio e specificare l&#39;autenticazione nome utente/password richiesta.

L’implementazione di riferimento implementa la seguente logica per la registrazione del dominio:

1. Determina il nome di dominio da assegnare a questo utente. Il nome dominio sarà * `namequalifier:username`* estratto dal token di autenticazione. Se non è presente alcun token di autenticazione, viene restituito l’errore DOM_AUTHENTICATION_REQUIRED (503).
1. Ricercare il nome di dominio in `DomainServerInfo` tabella. Se non viene trovata alcuna voce, inserire una voce nella tabella (i valori predefiniti sono obbligatori per l&#39;autenticazione, appartenenza massima al dominio=5).
1. Verifica se il dispositivo è già stato registrato con il dominio:

   1. Ricercare il nome dominio in `UserDomainMembership` tabella. Per ogni ID computer trovato, confronta con l’ID computer nella richiesta. Se si tratta di un nuovo computer, aggiungere una voce al `UserDomainMembership` tabella. Quindi, trova i record corrispondenti in `UserDomainRefCount` tabella. Se non esiste una voce per questo GUID computer, aggiungere un record.

   1. Se si tratta di un nuovo dispositivo e è già stato raggiunto il numero massimo di iscritti, viene restituito l&#39;errore DOM_LIMIT_FOUND (502).

1. Ricercare tutte le chiavi di dominio per questo dominio nella tabella DomainKeys.

   1. Se `DomainServerInfo` indica che è necessario eseguire il rollover delle chiavi, generare una nuova coppia di chiavi e salvarla in `DomainKeys` (con la versione della chiave 1 superiore alla chiave esistente più elevata) e reimpostare il flag &quot;Key Rollover Required&quot; in `DomainServerInfo`.

   1. Per ogni chiave di dominio, genera una credenziale di dominio.

L’implementazione di riferimento implementa la seguente logica per la cancellazione del dominio:

1. Determina il nome di dominio da assegnare a questo utente. Il nome di dominio sarà *namequalifier:nomeutente* estratto dal token di autenticazione. Se non è presente alcun token di autenticazione, viene restituito l’errore DOM_AUTHENTICATION_REQUIRED (503).
1. Ricercare il nome di dominio richiesto in `DomainServerInfo` tabella.
1. Ricercare il nome di dominio in `UserDomainMembership` tabella. Per ogni ID computer trovato, confronta con l’ID computer nella richiesta. Trova la voce corrispondente nella sezione `UserDomainRefCount` tabella. Se non viene trovata una voce corrispondente, viene restituito l&#39;errore DEREG_DENIED (401).

1. Se non si tratta di una richiesta di anteprima, elimina la voce da `UserDomainRefCount` tabella. Se nella tabella non sono presenti altre voci per il computer, eliminare la voce da `UserDomainMembership` e impostare il flag &quot;Key Rollover Required&quot; in `DomainServerInfo`.

In questo caso d’uso, a ogni utente è consentito registrare un numero limitato di computer, in modo da poter utilizzare l’ID completo del computer e `matches()` metodo per contare con precisione le macchine. Tuttavia, poiché l’utente può registrarsi più volte su questo computer (tramite più applicazioni AIR o lettori in diversi browser), il server deve anche mantenere un conteggio di riferimento, in modo che la de-registrazione possa essere conteggiata con precisione. La de-registrazione non può essere considerata completa finché non vengono restituiti tutti i token di dominio sul computer.
