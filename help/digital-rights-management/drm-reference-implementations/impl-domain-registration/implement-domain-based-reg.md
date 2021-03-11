---
title: Implementazione della registrazione del dominio basata sull'identità
description: Implementazione della registrazione del dominio basata sull'identità
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '47'
ht-degree: 0%

---


# Implementa la registrazione del dominio basato su identità{#implement-identity-based-domain-registration}

1. Crea un criterio DRM con registrazione obbligatoria del dominio.
1. Specifica l&#39;host e la porta del server per l&#39;URL del server di dominio.

   Nel file [!DNL .properties], imposta:

   ```
   policy.domain.url=https://[server:port] 
   ```

1. Rendi obbligatoria l’autenticazione con nome utente e password.

   Nel file [!DNL .properties], imposta:

   ```
   policy.domain.anonymous=false 
   ```
