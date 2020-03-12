---
seo-title: Implementazione della registrazione del dominio basata sull'identità
title: Implementazione della registrazione del dominio basata sull'identità
uuid: 4a71b2e0-d1a2-4d63-9cbd-980a292774ab
translation-type: tm+mt
source-git-commit: 4102780d0c7d0b96d120c1c2b3d14c47bc1b0e6f

---


# Implementazione della registrazione del dominio basata sull&#39;identità{#implement-identity-based-domain-registration}

1. Crea un criterio DRM con registrazione di dominio obbligatoria.
1. Specificate l&#39;host e la porta del server per l&#39;URL del server di dominio.

   Nel [!DNL .properties] file, impostate:

   ```
   policy.domain.url=https://[server:port] 
   ```

1. Rendere obbligatoria l&#39;autenticazione con un nome utente e una password.

   Nel [!DNL .properties] file, impostate:

   ```
   policy.domain.anonymous=false 
   ```
