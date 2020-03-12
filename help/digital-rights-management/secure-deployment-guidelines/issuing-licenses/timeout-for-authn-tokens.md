---
description: Tutti i token di autenticazione generati dall’SDK DRM di Adobe Primetime hanno un intervallo di timeout per proteggere la sicurezza dell’applicazione.
seo-description: Tutti i token di autenticazione generati dall’SDK DRM di Adobe Primetime hanno un intervallo di timeout per proteggere la sicurezza dell’applicazione.
seo-title: Timeout per token di autenticazione
title: Timeout per token di autenticazione
uuid: 2c2b0dad-0979-4d49-b109-2700ceb4d722
translation-type: tm+mt
source-git-commit: 5749142d42f7d7b36c96592955d1f71f6a7956fc

---


# Timeout per token di autenticazione{#timeout-for-authentication-tokens}

Tutti i token di autenticazione generati dall’SDK DRM di Adobe Primetime hanno un intervallo di timeout per proteggere la sicurezza dell’applicazione.

La scadenza per il token di autenticazione è specificata utilizza l&#39;SDK DRM di Primetime per gestire una richiesta di autenticazione. Una volta scaduto, il token non è più valido e l&#39;utente deve eseguire nuovamente l&#39;autenticazione con il server licenze.

Per ulteriori informazioni sulle richieste di autenticazione, vedere [AuthenticationHandler](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/authentication/AuthenticationHandler.html).
