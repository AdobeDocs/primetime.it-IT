---
title: Registrazione del dominio del gruppo di dispositivi
description: Registrazione del dominio del gruppo di dispositivi
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---


# Registrazione del dominio del gruppo di dispositivi{#device-group-domain-registration}

In alternativa al binding di una licenza a un dispositivo specifico, Adobe Access 3.0 e versioni successive supporta il binding di licenze a un dominio dispositivo. Più dispositivi possono unire un dominio e ricevere token di dominio. Dopo che un dispositivo nel dominio acquisisce una licenza, la licenza può essere trasferita a qualsiasi altro dispositivo del dominio e questi dispositivi possono riprodurre il contenuto senza acquisire una licenza direttamente dal server licenze.

Per supportare le licenze associate al dominio, il criterio deve specificare il server di dominio con cui il client deve registrarsi. Il criterio specifica inoltre i requisiti di autenticazione per il server di dominio (sia che sia consentito l’accesso anonimo, sia che il server richieda l’autenticazione con nome utente/password o personalizzata).

La registrazione del dominio e le licenze associate al dominio sono supportate dai client Adobe Access versione 3.0 e successive. Se un client precedente o un client Adobe Access 3.0 in Flash Player richiede una licenza per contenuti che supportano la registrazione del dominio, il server licenze può emettere una licenza utilizzando un criterio alternativo che supporta il binding a un dispositivo specifico.
