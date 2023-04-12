---
title: Implementazione dell'API senza client - Codici di errore / Messaggi con motivo probabile / causa
description: Implementazione dell'API senza client - Codici di errore / Messaggi con motivo probabile / causa
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---


# Implementazione dell&#39;API senza client - Codici di errore / Messaggi con motivo probabile / causa {#clientless-api-implementation--error-codes-messages-with-probable-reason-cause}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.

</br>


## Errore: Non autorizzato

### Cause:

1. Intestazione di autorizzazione mancante in POST
1. Problema con l&#39;intestazione di autorizzazione - verifica se il tempo di richiesta è in millisecondi.

## Errore: SC 400 durante l&#39;autenticazione

### Cause:

1. Il server non ha trovato il codice di registrazione, creato per un richiedente specifico e per un ambiente specifico.
1. È possibile che si verifichino problemi di scripting tra domini diversi
1. Lo spoofing appropriato deve essere aggiunto al file /etc/hosts

## Errore: 400 Richiesta non valida

### Cause:

1. URL non valido per POST/GET
1. SAMLAssertionParserException - Impossibile decrittografare l&#39;asserzione SAML crittografata al termine dell&#39;Adobe

## Errore: 403 Vietato

### Cause:

1. Troppe richieste rapide - una funzione della gestione API per prevenire attacchi DoS.
2. Se utilizzi un ambiente preuguale, aggiungi lo spoofing, altrimenti assicurati che lo spoofing sia stato rimosso dal file /etc/hosts

## Errore: Impossibile accedere alla pagina MVPD

### Cause:

1. Nome utente e password non corrispondenti 
2. L&#39;accesso potrebbe essere stato disattivato
3. Controlla se l&#39;accesso è per la produzione o lo staging


<!--

## Related Information

- [Clientless API Reference](/help/authentication/rest-api-reference.md)

-->