---
title: Registrazione dominio gruppo di dispositivi
description: Registrazione dominio gruppo di dispositivi
copied-description: true
exl-id: 1f3e9d26-c185-4d12-accf-aa74a313f890
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---

# Registrazione dominio gruppo di dispositivi{#device-group-domain-registration}

In alternativa al binding di una licenza a un dispositivo specifico, Adobe Access 3.0 e versioni successive supportano il binding delle licenze a un dominio del dispositivo. Più dispositivi possono essere aggiunti a un dominio e ricevere token di dominio. Dopo che un dispositivo del dominio ha acquisito una licenza, la licenza può essere trasferita a qualsiasi altro dispositivo del dominio e tali dispositivi possono riprodurre il contenuto senza acquisire una licenza direttamente dal server licenze.

Per supportare le licenze associate a dominio, il criterio deve specificare il server di dominio con cui il client deve registrarsi. I criteri specificheranno inoltre i requisiti di autenticazione per il server di dominio (se è consentito l&#39;accesso anonimo o se il server richiede nome utente/password o autenticazione personalizzata).

La registrazione del dominio e le licenze associate al dominio sono supportate dai client Adobe Access versione 3.0 e successive. Se un client precedente o un client Adobe Access 3.0 di Flash Player richiede una licenza per il contenuto che supporta la registrazione del dominio, il server licenze può rilasciare una licenza utilizzando un criterio alternativo che supporta l&#39;associazione a un dispositivo specifico.
