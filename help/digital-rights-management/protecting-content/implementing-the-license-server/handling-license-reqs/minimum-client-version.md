---
title: Versione client minima
description: Versione client minima
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---


# Versione minima client {#minimum-client-version}

Adobe Primetime DRM 2.0.2 e versioni successive introducono alcune nuove regole di utilizzo, che non sono comprese dai client Primetime DRM 2.0. Impostando la versione client minima supportata ( `HandlerConfiguration.setMinSupportedClientVersion()`), il server licenze può controllare il comportamento dei client meno recenti quando incontrano licenze con queste regole di utilizzo. In base a questa impostazione, il server può indicare se i client meno recenti possono ignorare le regole di utilizzo che non conoscono o se i client meno recenti non saranno in grado di utilizzare licenze con tali regole di utilizzo.

Ad esempio:

* Se la licenza specifica i requisiti di funzionalità del dispositivo ( [Funzionalità del dispositivo necessarie per riprodurre contenuto protetto](../../../protecting-content/introduction/usage-rules/runtime-application-restrictions/device-capabilities.md)), i client DRM Primetime 2.0.2 e versioni successive possono applicare tali requisiti.
* Se il server licenze non desidera che il contenuto venga riprodotto su client che non conoscono i requisiti di funzionalità del dispositivo , imposta la versione client minima supportata su 2 (per 2.0.2). Questo impedirà al server di rilasciare licenze ai client DRM Primetime prima della versione 2.0.2. La versione minima del client viene applicata anche se la licenza viene trasferita da un client a un altro.
* Se il server licenze desidera consentire ai client meno recenti di ignorare i requisiti di funzionalità del dispositivo, imposta la versione client minima supportata su 1 (per Primetime DRM 2.0). Il server rilascia quindi una licenza a qualsiasi client versione 2.0 e successiva. Se il client aggiorna o trasferisce la licenza a un altro client con versione 2.0.2 o successiva, i requisiti di funzionalità del dispositivo nella licenza vengono quindi applicati perché il client può quindi supportare tale regola di utilizzo.

