---
description: Tutti i token di autenticazione generati dall’SDK DRM di Adobe Primetime hanno un intervallo di timeout per proteggere la sicurezza dell’applicazione.
title: Timeout per token di autenticazione
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---


# Timeout per token di autenticazione{#timeout-for-authentication-tokens}

Tutti i token di autenticazione generati dall’SDK DRM di Adobe Primetime hanno un intervallo di timeout per proteggere la sicurezza dell’applicazione.

La scadenza per il token di autenticazione è specificata utilizza l’SDK DRM di Primetime quando gestisci una richiesta di autenticazione. Una volta scaduto, il token non è più valido e l’utente deve eseguire nuovamente l’autenticazione con il server licenze.

Per ulteriori informazioni sulle richieste di autenticazione, consulta [AuthenticationHandler](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/authentication/AuthenticationHandler.html).
