---
title: Autenticazione utente
description: Autenticazione utente
copied-description: true
exl-id: a0dd7d81-2249-4845-94da-53b755d6cd7c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---

# Autenticazione utente{#user-authentication}

Una richiesta di accesso di Adobe può contenere un token di autenticazione.

Se è stata utilizzata l’autenticazione nome utente/password, la richiesta può contenere `AuthenticationToken` generato da `AuthenticationHandler`. Per accedere e verificare il token, utilizza `RequestMessageBase.getAuthenticationToken()`. Per avviare una richiesta di nome utente/password sul client, utilizzare `DRMManager.authenticate()` API ActionScript o iOS.

Se il client e il server utilizzano un meccanismo di autenticazione personalizzato, il client ottiene un token di autenticazione tramite un altro canale e imposta il token di autenticazione personalizzato utilizzando `DRMManager.setAuthenticationToken` API ActionScript 3.0. Utilizzare `RequestMessageBase.getRawAuthenticationToken()` per ottenere il token di autenticazione personalizzato. L’implementazione del server è responsabile di determinare se il token di autenticazione personalizzato è valido.
