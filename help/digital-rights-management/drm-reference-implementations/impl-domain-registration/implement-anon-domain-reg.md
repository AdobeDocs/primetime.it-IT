---
seo-title: Implementazione della registrazione del dominio anonima
title: Implementazione della registrazione del dominio anonima
uuid: 330d32fd-8c23-40f9-949b-635e5a9acc86
translation-type: tm+mt
source-git-commit: 4102780d0c7d0b96d120c1c2b3d14c47bc1b0e6f

---


# Implementazione della registrazione del dominio anonima{#implement-anonymous-domain-registration}

1. Create un criterio DRM che specifica che è richiesta la registrazione del dominio.
1. Specificate l’URL del server di dominio come:

   ```
   https://[host:port]/flashaccess/domainserver/domainname/
   ```

1. Rendere obbligatoria l&#39;autenticazione anonima.

   Nel [!DNL .properties] file, impostate:

   ```
   policy.domain.anonymous=true 
   ```
