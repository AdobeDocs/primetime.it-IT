---
title: Autenticazione utente
description: Autenticazione utente
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---


# Autenticazione utente {#user-authentication}

Una richiesta Adobe Primetime DRM può contenere un token di autenticazione.

Se è stata utilizzata l’autenticazione nome utente/password, la richiesta può includere `AuthenticationToken` generato da `AuthenticationHandler`. Se desideri accedere e verificare il token, devi utilizzare `RequestMessageBase.getAuthenticationToken()`. Per avviare una richiesta di nome utente/password sul client, utilizzare `DRMManager.authenticate()` API ActionScript o iOS.

Se il client e il server utilizzano un meccanismo di autenticazione personalizzato, il client ottiene un token di autenticazione tramite un altro canale e imposta il token di autenticazione personalizzato utilizzando `DRMManager.setAuthenticationToken` API ActionScript 3.0. Utilizzare `RequestMessageBase.getRawAuthenticationToken()` per ottenere il token di autenticazione personalizzato. L’implementazione del server determina se il token di autenticazione personalizzato è valido.
