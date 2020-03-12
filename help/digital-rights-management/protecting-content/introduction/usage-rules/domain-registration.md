---
seo-title: Registrazione del dominio del gruppo di dispositivi
title: Registrazione del dominio del gruppo di dispositivi
uuid: 221bf6c3-0568-443d-b761-64715a57ada6
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Registrazione del dominio del gruppo di dispositivi{#device-group-domain-registration}

In alternativa al binding di una licenza con un dispositivo specifico, Primetime DRM 3.0 o versione successiva supporta il binding delle licenze a un dominio dispositivo.

Più dispositivi possono unirsi a un dominio e ricevere token di dominio. Dopo che un dispositivo del dominio acquisisce una licenza, la licenza può essere trasferita a qualsiasi altro dispositivo del dominio e tali dispositivi possono riprodurre il contenuto senza acquisire una licenza direttamente dal server licenze.

Se desiderate supportare licenze con binding di dominio, il criterio DRM di Primetime deve specificare il server di dominio con cui il client deve registrarsi. Il criterio DRM di Primetime deve inoltre specificare i requisiti di autenticazione per il server di dominio, sia che l&#39;accesso anonimo sia abilitato, sia che il server richieda autenticazione tramite nome utente/password o personalizzata.

Le licenze per la registrazione del dominio e le licenze con binding di dominio sono supportate dai client DRM di Primetime versione 3.0 o successiva. Se un client precedente o un client Adobe Primetime 3.0 in Flash Player richiede una licenza per il contenuto che supporta la registrazione del dominio, il server licenze può rilasciare una licenza che utilizza un criterio DRM Primetime alternativo per supportare il binding a un dispositivo specifico.
