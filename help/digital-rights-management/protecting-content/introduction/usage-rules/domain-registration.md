---
title: Registrazione dominio gruppo di dispositivi
description: Registrazione dominio gruppo di dispositivi
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---

# Registrazione dominio gruppo di dispositivi{#device-group-domain-registration}

In alternativa al binding di una licenza a un dispositivo specifico, Primetime DRM 3.0 o versione successiva supporta il binding delle licenze a un dominio dispositivo.

Più dispositivi possono essere aggiunti a un dominio e ricevere token di dominio. Dopo che un dispositivo del dominio ha acquisito una licenza, la licenza può essere trasferita a qualsiasi altro dispositivo del dominio e tali dispositivi possono riprodurre il contenuto senza acquisire una licenza direttamente dal server licenze.

Se si desidera supportare licenze associate a dominio, il criterio DRM di Primetime deve specificare il server di dominio con cui il client deve registrarsi. Il criterio DRM di Primetime deve inoltre specificare i requisiti di autenticazione per il server di dominio, sia che l&#39;accesso anonimo sia abilitato o che il server richieda nome utente/password o autenticazione personalizzata.

La registrazione del dominio e le licenze associate al dominio sono supportate dai client DRM Primetime versione 3.0 o successiva. Se un client precedente o un client Adobe Primetime 3.0 di Flash Player richiede una licenza per il contenuto che supporta la registrazione del dominio, il server licenze può rilasciare una licenza che utilizza un criterio DRM Primetime alternativo per supportare l&#39;associazione a un dispositivo specifico.
