---
title: Implementare la registrazione del dominio anonimo
description: Implementare la registrazione del dominio anonimo
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '37'
ht-degree: 0%

---


# Implementa la registrazione anonima del dominio{#implement-anonymous-domain-registration}

1. Crea un criterio DRM che specifica che è richiesta la registrazione del dominio.
1. Specifica l’URL del server di dominio come:

   ```
   https://[host:port]/flashaccess/domainserver/domainname/
   ```

1. Rendi obbligatoria l&#39;autenticazione anonima.

   Nel file [!DNL .properties], imposta:

   ```
   policy.domain.anonymous=true 
   ```
