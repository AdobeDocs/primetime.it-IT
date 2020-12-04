---
seo-title: Autenticazione utente
title: Autenticazione utente
uuid: 5cbd76b9-ff64-4a4b-8cfd-54f05c04eaa3
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---


# Autenticazione utente {#user-authentication}

Una richiesta  Adobe Primetime DRM può contenere un token di autenticazione.

Se è stata utilizzata l&#39;autenticazione tramite nome utente/password, la richiesta potrebbe includere un `AuthenticationToken` generato da `AuthenticationHandler`. Per accedere e verificare il token, è necessario utilizzare `RequestMessageBase.getAuthenticationToken()`. Per avviare una richiesta di nome utente/password sul client, utilizzate l&#39;API `DRMManager.authenticate()`  ActionScript o iOS.

Se il client e il server utilizzano un meccanismo di autenticazione personalizzato, il client ottiene un token di autenticazione tramite un altro canale e imposta il token di autenticazione personalizzato utilizzando l&#39;API `DRMManager.setAuthenticationToken`  ActionScript 3.0. Utilizzate `RequestMessageBase.getRawAuthenticationToken()` per ottenere il token di autenticazione personalizzato. L&#39;implementazione del server determina se il token di autenticazione personalizzato è valido.
