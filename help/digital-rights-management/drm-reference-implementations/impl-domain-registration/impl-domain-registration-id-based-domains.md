---
title: Logica di registrazione del dominio basata su identità
description: Logica di registrazione del dominio basata su identità
copied-description: true
exl-id: 6e391fce-00b4-45cf-b785-3b0ec734a11e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---

# Logica di registrazione del dominio basata su identità{#identity-based-domain-registration-logic}

## Logica di registrazione del dominio {#section_149C247458954877AF158B4A09A8526B}

L’implementazione di riferimento applica la seguente logica per la registrazione dei domini basati su identità:

1. Determina il nome di dominio da assegnare a un utente designato.

   Il nome di dominio ( `namequalifier:username`) viene estratto dal token di autenticazione. Se un token non è disponibile, viene generato un errore.
1. Cercare il nome di dominio in `DomainServerInfo` tabella.

   Se non viene trovata alcuna voce, inserire una voce. I valori predefiniti sono:

   * `authentication required`
   * `max domain membership=5`

   .

1. Per verificare che il dispositivo sia stato registrato con il dominio:

   1. Cercare `domainname` nel `UserDomainMembership` tabella:

      1. Per ogni ID computer individuato, confronta l’ID con l’ID computer nella richiesta.
      1. Se si tratta di un nuovo computer, aggiungere una voce al `UserDomainMembership` tabella.
      1. Cerca i record corrispondenti in `UserDomainRefCount` tabella.
      1. Se non esiste una voce per questo GUID computer, aggiungere un record.
   1. Se si tratta di un nuovo dispositivo, e `Max Membership` è stato raggiunto il valore, viene restituito un errore.


1. Cerca tutte le chiavi di dominio per questo dominio nel `DomainKeys` tabella:

   1. Se `DomainServerInfo` indica che è necessario eseguire il rollover delle chiavi e generare una nuova coppia di chiavi,
   1. Salva la coppia in `DomainKeys` con una versione di chiave superiore di una a quella della chiave esistente più elevata.
   1. Reimposta `Key Rollover Required` contrassegna in `DomainServerInfo`.

   1. Per ogni chiave di dominio, genera una credenziale di dominio.

## Logica di annullamento registrazione dominio {#section_78AFA63D8F744BE6BCA10A51B4FCBA22}

L’implementazione di riferimento applica la seguente logica per la cancellazione del dominio basata su identità:

1. Determina il nome di dominio da assegnare a questo utente.

   Il nome di dominio è `namequalifier:username`, estratto dal token di autenticazione. Se non è disponibile alcun token, viene restituito un errore `DOM_AUTHENTICATION_REQUIRED (503)` si verifica.
1. Cercare il nome di dominio richiesto in `DomainServerInfo` tabella.
1. Cercare il nome di dominio in `UserDomainMembership` tabella.
1. Confronta ogni ID computer trovato con l’ID computer nella richiesta.
1. Individuare la voce corrispondente nella `UserDomainRefCount` tabella.

   Se non si trova una voce corrispondente, viene restituito un errore.

1. Se non si tratta di una richiesta di anteprima, elimina la voce dalla `UserDomainRefCount` tabella.
1. Se nella tabella non sono presenti voci aggiuntive per il computer, eliminare la voce da `UserDomainMembership` e imposta [!DNL Key Rollover Required] contrassegno nel `DomainServerInfo` proprietà.

Ogni utente può registrare un numero limitato di computer, in modo da poter utilizzare l&#39;ID macchina completo e `matches()` metodo di conteggio delle macchine. Poiché un utente può registrarsi più volte, tramite più applicazioni AIR o lettori in diversi browser, il server deve mantenere un conteggio di riferimento in modo che possa essere conteggiata anche la cancellazione.

>[!NOTE]
>
>La cancellazione dal registro non è completa finché non vengono restituiti tutti i token di dominio del computer.
