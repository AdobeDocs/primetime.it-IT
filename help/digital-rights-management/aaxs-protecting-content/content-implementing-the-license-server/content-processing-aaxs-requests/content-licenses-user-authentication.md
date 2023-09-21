---
title: Autenticazione utente
description: Autenticazione utente
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---

# Autenticazione utente{#user-authentication}

Una richiesta di accesso di Adobe può contenere un token di autenticazione.

Se è stata utilizzata l’autenticazione nome utente/password, la richiesta può contenere `AuthenticationToken` generato da `AuthenticationHandler`. Per accedere e verificare il token, utilizza `RequestMessageBase.getAuthenticationToken()`. Per avviare una richiesta di nome utente/password sul client, utilizzare `DRMManager.authenticate()` API ActionScript o iOS.

Se il client e il server utilizzano un meccanismo di autenticazione personalizzato, il client ottiene un token di autenticazione tramite un altro canale e imposta il token di autenticazione personalizzato utilizzando `DRMManager.setAuthenticationToken` API ActionScript 3.0. Utilizzare `RequestMessageBase.getRawAuthenticationToken()` per ottenere il token di autenticazione personalizzato. L’implementazione del server è responsabile di determinare se il token di autenticazione personalizzato è valido.
