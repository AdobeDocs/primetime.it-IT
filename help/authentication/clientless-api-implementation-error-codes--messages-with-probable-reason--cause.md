---
title: Implementazione API senza client - Codici di errore/messaggi con motivo/causa probabile
description: Implementazione API senza client - Codici di errore/messaggi con motivo/causa probabile
exl-id: 616e35fc-9b72-422b-9a05-e6248bd52490
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# Implementazione API senza client - Codici di errore/messaggi con motivo/causa probabile {#clientless-api-implementation--error-codes-messages-with-probable-reason-cause}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente di Adobe. Non è consentito alcun uso non autorizzato.

</br>


## Errore: non autorizzato

### Cause:

1. Intestazione di autorizzazione mancante nel POST
1. Problema con l’intestazione di autorizzazione: verifica se il tempo della richiesta è in millisecondi.

## Errore: SC 400 durante l’autenticazione

### Cause:

1. Il server non ha trovato il codice di registrazione, che è stato creato per un richiedente e un ambiente specifici.
1. Potresti riscontrare problemi di scripting tra domini
1. Il spoofing corretto deve essere aggiunto al file /etc/hosts

## Errore: richiesta 400 non valida

### Cause:

1. URL in formato non valido per POST/GET
1. SAMLAssertionParserException: impossibile decrittografare l’asserzione SAML crittografata alla fine di Adobe

## Errore: 403 - Non consentito

### Cause:

1. Troppe richieste rapide: una funzione della gestione API per prevenire gli attacchi DoS.
2. Se utilizzi l’ambiente preuguale, aggiungi lo spoofing, altrimenti assicurati che lo spoofing sia stato rimosso dal file /etc/hosts

## Errore: impossibile accedere alla pagina MVPD

### Cause:

1. Nome utente e password non corrispondono 
2. L’accesso potrebbe essere stato disabilitato
3. Controlla se l&#39;accesso è per la produzione o la gestione temporanea


<!--

## Related Information

- [Clientless API Reference](/help/authentication/rest-api-reference.md)

-->
