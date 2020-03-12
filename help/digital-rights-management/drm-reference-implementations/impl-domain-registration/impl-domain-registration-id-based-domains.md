---
description: 'null'
seo-description: 'null'
seo-title: Logica di registrazione del dominio basata su identità
title: Logica di registrazione del dominio basata su identità
uuid: bc13f7c2-9a20-4f80-b96f-05f7a0fcc343
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Logica di registrazione del dominio basata su identità{#identity-based-domain-registration-logic}

## Logica di registrazione del dominio {#section_149C247458954877AF158B4A09A8526B}

L&#39;implementazione di riferimento applica la seguente logica per la registrazione del dominio basata sull&#39;identità:

1. Determinare il nome di dominio da assegnare a un utente designato.

   Il nome di dominio ( `namequalifier:username`) viene estratto dal token di autenticazione. Se un token non è disponibile, viene generato un errore.
1. Cerca il nome del dominio nella `DomainServerInfo` tabella.

   Se non viene trovata alcuna voce, inserire una voce. I valori predefiniti sono:

   * `authentication required`
   * `max domain membership=5`
   .

1. Per verificare che il dispositivo sia stato registrato nel dominio:

   1. Cercare `domainname` nella `UserDomainMembership` tabella:

      1. Per ciascun ID computer individuato, confrontate l’ID con l’ID computer nella richiesta.
      1. Se si tratta di un nuovo computer, aggiungere una voce alla `UserDomainMembership` tabella.
      1. Cercare i record corrispondenti nella `UserDomainRefCount` tabella.
      1. Se non esiste una voce per il GUID del computer, aggiungere un record.
   1. Se si tratta di un nuovo dispositivo e il `Max Membership` valore è stato raggiunto, restituisce un errore.


1. Cerca tutte le chiavi di dominio per questo dominio nella `DomainKeys` tabella:

   1. Se `DomainServerInfo` indica che è necessario scorrere i tasti, generare una nuova coppia di chiavi,
   1. Salvare la coppia nella `DomainKeys` tabella, con una versione chiave superiore di uno rispetto alla chiave più alta esistente.
   1. Reimpostare il `Key Rollover Required` flag in `DomainServerInfo`.

   1. Per ogni chiave di dominio, genera una credenziale di dominio.

## Logica di deregistrazione del dominio {#section_78AFA63D8F744BE6BCA10A51B4FCBA22}

L&#39;implementazione di riferimento applica la seguente logica per la deregistrazione del dominio basata sull&#39;identità:

1. Determinare il nome di dominio da assegnare a questo utente.

   Il nome di dominio è `namequalifier:username`, che viene estratto dal token di autenticazione. Se non è disponibile alcun token, `DOM_AUTHENTICATION_REQUIRED (503)` viene restituito un errore.
1. Cerca il nome di dominio richiesto nella `DomainServerInfo` tabella.
1. Cerca il nome del dominio nella `UserDomainMembership` tabella.
1. Confrontare l&#39;ID computer trovato con l&#39;ID computer della richiesta.
1. Individuare la voce corrispondente nella `UserDomainRefCount` tabella.

   Se una voce corrispondente non si trova, restituisce un errore.

1. Se non si tratta di una richiesta di anteprima, eliminate la voce dalla `UserDomainRefCount` tabella.
1. Se la tabella non contiene voci aggiuntive per il computer, eliminare la voce `UserDomainMembership` e impostare il [!DNL Key Rollover Required] flag nella `DomainServerInfo` proprietà.

Ogni utente può registrare un numero limitato di computer, in modo da poter utilizzare l&#39;ID computer completo e il `matches()` metodo per contare i computer. Poiché un utente può registrarsi più volte, attraverso più applicazioni AIR o lettori in browser diversi, il server deve mantenere un conteggio di riferimento in modo da poter contare anche la deregistrazione.

>[!NOTE]
>
>La deregistrazione non è completa finché non vengono consegnati tutti i token di dominio presenti nel computer.

