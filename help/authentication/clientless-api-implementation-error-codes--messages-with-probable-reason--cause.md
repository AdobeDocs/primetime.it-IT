---
title: Implementazione API clientless-codici/messaggi Errore con probabile motivo/causa
description: Implementazione API clientless-codici/messaggi Errore con probabile motivo/causa
exl-id: 616e35fc-9b72-422b-9a05-e6248bd52490
source-git-commit: 84a16ce775a0aab96ad954997c008b5265e69283
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# Implementazione API clientless-codici/messaggi Errore con probabile motivo/causa {#clientless-api-implementation--error-codes-messages-with-probable-reason-cause}

>[!NOTE]
>
>I contenuto in questa pagina sono forniti solo a scopo informativo. L&#39;utilizzo di questa API richiede una licenza corrente da Adobe Systems. Non è consentito alcun uso non autorizzato.

</br>


## Errore: non autorizzato

### Cause:

1. Intestazione di autorizzazione mancante nella POST
1. Problema con l&#39;intestazione Authorization-Controlla se richiesta tempo è in millisecondi.

## Errore: SC 400 durante l&#39;autenticazione

### Cause:

1. Il server non ha trovato il codice registrazione, che è stato creato per un richiedente e un ambiente specifici.
1. Potresti essere in esecuzione in problemi di scripting tra domini diversi
1. È necessario aggiungere un corretto spoofing al file/etc/hosts

## Errore: 400 richiesta non valida

### Cause:

1. URL non valido per POST/GET
1. SAMLAssertionParserException – l&#39;asserzione SAML crittografata non è stata decrittografata alla fine di Adobe Systems

## Errore: 403 Forbidden

### Cause:

1. Troppe richieste rapide-una funzione della gestione delle API per prevenire gli attacchi DoS.
2. Se utilizzi un ambiente PreQual, Aggiungi lo spoofing, altrimenti assicurati che lo spoofing sia stato rimosso dal file/etc/hosts

## Errore: Impossibile accedere alla pagina MVPD

### Cause:

1. Nome utente e password non corrispondono
2. L&#39;accesso potrebbe essere stato disattivato
3. Controlla se l&#39;accesso è per la produzione o la gestione temporanea


<!--

## Related Information

- [Clientless API Reference](/help/authentication/rest-api-reference.md)

-->
