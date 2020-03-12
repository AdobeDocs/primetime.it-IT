---
seo-title: Registrazione del dominio del gruppo di dispositivi
title: Registrazione del dominio del gruppo di dispositivi
uuid: fd559175-2c3c-4d71-bfa1-8de9907d2b7c
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Registrazione del dominio del gruppo di dispositivi{#device-group-domain-registration}

In alternativa al binding di una licenza con un dispositivo specifico, Adobe Access 3.0 e versioni successive supporta il binding delle licenze a un dominio dispositivo. Più dispositivi possono unirsi a un dominio e ricevere token di dominio. Dopo che un dispositivo del dominio acquisisce una licenza, la licenza può essere trasferita a qualsiasi altro dispositivo del dominio e tali dispositivi possono riprodurre il contenuto senza acquisire una licenza direttamente dal server licenze.

Per supportare le licenze con binding di dominio, il criterio deve specificare il server di dominio con cui il client deve registrarsi. Il criterio specifica inoltre i requisiti di autenticazione per il server di dominio (sia che sia consentito l&#39;accesso anonimo, sia che il server richieda l&#39;autenticazione tramite nome utente/password o personalizzata).

Le licenze per la registrazione del dominio e quelle associate al dominio sono supportate dai client Adobe Access versione 3.0 e successive. Se un client precedente o un client Adobe Access 3.0 in Flash Player richiede una licenza per il contenuto che supporta la registrazione del dominio, il server licenze può rilasciare una licenza utilizzando un criterio alternativo che supporta il binding a un dispositivo specifico.
