---
title: Timeout per token di autenticazione
description: Timeout per token di autenticazione
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---


# Timeout per token di autenticazione{#timeout-for-authentication-tokens}

Tutti i token di autenticazione generati dall’SDK di Adobe Access hanno un intervallo di timeout per proteggere la sicurezza dell’applicazione. La scadenza per il token di autenticazione è specificata utilizza l’SDK di Adobe Access quando gestisci una richiesta di autenticazione. Una volta passata la scadenza, il token di autenticazione non è più valido e l’utente deve effettuare nuovamente l’autenticazione con il server licenze.

Per ulteriori informazioni sulle richieste di autenticazione, consulta AuthenticationHandler in *Riferimento API di accesso Adobe*.
