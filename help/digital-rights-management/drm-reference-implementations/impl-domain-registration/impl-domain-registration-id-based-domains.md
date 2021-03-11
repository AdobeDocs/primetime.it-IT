---
title: Logica di registrazione del dominio basata su identità
description: Logica di registrazione del dominio basata su identità
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---


# Logica di registrazione del dominio basata su identità{#identity-based-domain-registration-logic}

## Logica di registrazione del dominio {#section_149C247458954877AF158B4A09A8526B}

L’implementazione di riferimento applica la seguente logica per la registrazione del dominio basato sull’identità:

1. Determinare il nome di dominio da assegnare a un utente designato.

   Il nome di dominio ( `namequalifier:username`) viene estratto dal token di autenticazione. Se un token non è disponibile, viene generato un errore.
1. Cerca il nome di dominio nella tabella `DomainServerInfo`.

   Se non viene trovata alcuna voce, inserire una voce. I valori predefiniti sono:

   * `authentication required`
   * `max domain membership=5`

   .

1. Per verificare che il dispositivo sia stato registrato nel dominio:

   1. Cerca il `domainname` nella tabella `UserDomainMembership`:

      1. Per ogni ID computer individuato, confronta l’ID con l’ID computer nella richiesta.
      1. Se si tratta di un nuovo computer, aggiungere una voce alla tabella `UserDomainMembership`.
      1. Cerca i record corrispondenti nella tabella `UserDomainRefCount`.
      1. Se non esiste una voce per questo GUID computer, aggiungere un record.
   1. Se si tratta di un nuovo dispositivo e il valore `Max Membership` è stato raggiunto, restituisce l’errore .


1. Cerca tutte le chiavi di dominio per questo dominio nella tabella `DomainKeys`:

   1. Se `DomainServerInfo` indica che è necessario eseguire il rollover delle chiavi, genera una nuova coppia di chiavi,
   1. Salvare la coppia nella tabella `DomainKeys` con una versione chiave superiore alla chiave esistente più alta.
   1. Reimposta il flag `Key Rollover Required` in `DomainServerInfo`.

   1. Per ogni chiave di dominio, genera una credenziale di dominio.

## Logica di cancellazione del dominio {#section_78AFA63D8F744BE6BCA10A51B4FCBA22}

L&#39;implementazione di riferimento applica la seguente logica per la deregistrazione del dominio basato sull&#39;identità:

1. Determinare il nome di dominio da assegnare a questo utente.

   Il nome di dominio è `namequalifier:username`, che viene estratto dal token di autenticazione. Se non è disponibile alcun token, si verifica l’errore di ritorno `DOM_AUTHENTICATION_REQUIRED (503)`.
1. Cerca il nome di dominio richiesto nella tabella `DomainServerInfo`.
1. Cerca il nome di dominio nella tabella `UserDomainMembership`.
1. Confronta ogni ID macchina trovato con l&#39;ID macchina nella richiesta.
1. Individua la voce corrispondente nella tabella `UserDomainRefCount`.

   Se non si trova una voce corrispondente, restituisce l’errore .

1. Se non si tratta di una richiesta di anteprima, elimina la voce dalla tabella `UserDomainRefCount`.
1. Se non sono presenti voci aggiuntive in quella tabella per il computer, eliminare la voce da `UserDomainMembership` e impostare il flag [!DNL Key Rollover Required] nella proprietà `DomainServerInfo`.

Ogni utente può registrare un numero limitato di computer, in modo da poter utilizzare l&#39;ID macchina completo e il metodo `matches()` per contare i computer. Poiché un utente può registrarsi più volte, attraverso più applicazioni AIR o lettori in diversi browser, il server deve mantenere un conteggio di riferimento in modo che possa essere conteggiata anche la cancellazione della registrazione.

>[!NOTE]
>
>La cancellazione della registrazione non è completa finché non vengono consegnati tutti i token di dominio sul computer.

