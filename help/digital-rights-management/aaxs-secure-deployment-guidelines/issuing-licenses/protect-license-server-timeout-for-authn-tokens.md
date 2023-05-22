---
title: Timeout per i token di autenticazione
description: Timeout per i token di autenticazione
copied-description: true
exl-id: ee9c5b2c-6a79-499c-bd60-718e33bc3a9b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---

# Timeout per i token di autenticazione{#timeout-for-authentication-tokens}

Tutti i token di autenticazione generati dall’SDK di accesso Adobe dispongono di un intervallo di timeout per proteggere la sicurezza dell’applicazione. La scadenza del token di autenticazione è specificata. Utilizza l’SDK di accesso Adobe per gestire una richiesta di autenticazione. Dopo la scadenza, il token di autenticazione non è più valido e l’utente deve autenticarsi di nuovo con il server licenze.

Per ulteriori informazioni sulle richieste di autenticazione, consulta AuthenticationHandler in *Riferimento API per l’accesso agli Adobi*.
