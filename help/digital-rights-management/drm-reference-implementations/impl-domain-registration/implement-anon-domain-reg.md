---
title: Implementare la registrazione di domini anonimi
description: Implementare la registrazione di domini anonimi
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '37'
ht-degree: 0%

---

# Implementare la registrazione di domini anonimi{#implement-anonymous-domain-registration}

1. Creare un criterio DRM che specifichi che la registrazione del dominio è obbligatoria.
1. Specifica l’URL del server di dominio come:

   ```
   https://[host:port]/flashaccess/domainserver/domainname/
   ```

1. Rendi obbligatoria l’autenticazione anonima.

   Nel tuo [!DNL .properties] file, imposta:

   ```
   policy.domain.anonymous=true 
   ```
