---
title: Implementazione API Clientless - Codici Errore / Messaggi con probabile motivo / causa
description: Implementazione API Clientless - Codici Errore / Messaggi con probabile motivo / causa
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# Implementazione API Clientless - Codici Errore / Messaggi con probabile motivo / causa {#clientless-api-implementation--error-codes-messages-with-probable-reason-cause}

>[!NOTE]
>
>Il contenuto presente in questa pagina è fornito solo a scopo informativo. L&#39;utilizzo di questa API richiede una licenza valida da Adobe Systems. Non è consentito alcun uso non autorizzato.

</br>


## Errore: Non autorizzato

### Cause:

1. Intestazione autorizzazione mancante nel POST
1. Problema con l&#39;intestazione di autorizzazione: controlla se richiesta tempo è in millisecondi.

## Errore: SC 400 durante l&#39;autenticazione

### Cause:

1. Il server non ha trovato il codice registrazione, che è stato creato per un richiedente e un ambiente specifici.
1. Potresti incorrere in problemi di scripting tra domini diversi
1. Lo spoofing corretto dovrebbe essere aggiunto al file /etc/hosts

## Errore: 400 Richiesta non valida

### Cause:

1. URL non valido per POST/GET
1. SAMLAssertionParserException – L&#39;asserzione SAML crittografata non poteva essere decrittografata alla fine dell Adobe Systems

## Errore: 403 Proibito

### Cause:

1. Troppe richieste rapide: una funzionalità della gestione API per prevenire attacchi DoS.
2. Se usi l&#39;ambiente prequal, aggiungi lo spoofing, altrimenti assicurati che lo spoofing sia stato rimosso dal file /etc/hosts

## Errore: Impossibile accedere alla pagina MVPD

### Cause:

1. Nome utente e password non corrispondono
2. L&#39;accesso potrebbe essere stato disabilitato
3. Controlla se l&#39;accesso è per la produzione o la gestione temporanea


<!--

## Related Information

- [Clientless API Reference](/help/authentication/rest-api-reference.md)

-->
