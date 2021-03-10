---
title: Registrazione del dominio del gruppo di dispositivi
description: Registrazione del dominio del gruppo di dispositivi
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---


# Registrazione del dominio del gruppo di dispositivi{#device-group-domain-registration}

In alternativa al binding di una licenza a un dispositivo specifico, Primetime DRM 3.0 o versioni successive supporta il binding di licenze a un dominio dispositivo.

Più dispositivi possono unire un dominio e ricevere token di dominio. Dopo che un dispositivo nel dominio acquisisce una licenza, la licenza può essere trasferita a qualsiasi altro dispositivo del dominio e questi dispositivi possono riprodurre il contenuto senza acquisire una licenza direttamente dal server licenze.

Se desideri supportare licenze associate a un dominio, il criterio DRM di Primetime deve specificare il server di dominio con cui il client deve registrarsi. Il criterio DRM di Primetime deve inoltre specificare i requisiti di autenticazione per il server di dominio, indipendentemente dal fatto che l&#39;accesso anonimo sia abilitato o che il server richieda l&#39;autenticazione con nome utente/password o personalizzata.

La registrazione del dominio e le licenze associate al dominio sono supportate dai client DRM di Primetime versione 3.0 o successiva. Se un client precedente o un client Adobe Primetime 3.0 in Flash Player richiede una licenza per contenuti che supportano la registrazione del dominio, il server licenze può rilasciare una licenza che utilizza un criterio DRM alternativo di Primetime per supportare il binding a un dispositivo specifico.
