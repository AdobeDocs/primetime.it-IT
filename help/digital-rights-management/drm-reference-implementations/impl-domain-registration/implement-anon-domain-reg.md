---
title: Implementare la registrazione di domini anonimi
description: Implementare la registrazione di domini anonimi
copied-description: true
exl-id: 304cfe6f-0917-42ef-a49a-e6c4bc9c10d0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
