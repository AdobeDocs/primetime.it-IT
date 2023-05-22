---
title: Implementare la registrazione dei domini basata su identità
description: Implementare la registrazione dei domini basata su identità
copied-description: true
exl-id: e2f826a8-eea5-4d5f-ac4d-401d7a6c5373
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '47'
ht-degree: 0%

---

# Implementare la registrazione dei domini basata su identità{#implement-identity-based-domain-registration}

1. Creare un criterio DRM con registrazione del dominio obbligatoria.
1. Specificare l&#39;host e la porta del server per l&#39;URL del server di dominio.

   Nel tuo [!DNL .properties] file, imposta:

   ```
   policy.domain.url=https://[server:port] 
   ```

1. Rendi obbligatoria l’autenticazione con nome utente e password.

   Nel tuo [!DNL .properties] file, imposta:

   ```
   policy.domain.anonymous=false 
   ```
