---
title: Versione minima client
description: Versione minima client
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---


# Versione minima del client {#minimum-client-version}

In Adobe Access 2.0.2 e versioni successive sono state introdotte alcune nuove regole di utilizzo, che non sono comprese dai client Adobe Access 2.0. Impostando la versione client minima supportata ( `HandlerConfiguration.setMinSupportedClientVersion()`), il server licenze può controllare il comportamento dei client meno recenti quando incontrano licenze con queste regole di utilizzo. In base a questa impostazione, il server può indicare se i client meno recenti possono ignorare le regole di utilizzo che non conoscono o se i client meno recenti non saranno in grado di utilizzare licenze con tali regole di utilizzo.

Ad esempio:

* Se la licenza specifica i requisiti di funzionalità del dispositivo ( [Funzionalità del dispositivo necessarie per riprodurre contenuto protetto](../../../aaxs-protecting-content/content-introduction/content-usage-rules/content-runtime-application-restrictions/content-device-capabilities.md)), i client Adobe Access 2.0.2 e versioni successive possono applicare tali requisiti.
* Se il server licenze non desidera che il contenuto venga riprodotto su client che non conoscono i requisiti di funzionalità del dispositivo , imposta la versione client minima supportata su 2 (per 2.0.2). Questo impedirà al server di rilasciare licenze ai client Adobe Access prima della versione 2.0.2. La versione minima del client verrà applicata anche se la licenza viene trasferita da un client a un altro.
* Se il server licenze desidera consentire ai client meno recenti di ignorare i requisiti di funzionalità del dispositivo, impostare la versione client minima supportata su 1 (ad Adobe Access 2.0). Il server rilascerà una licenza per qualsiasi client versione 2.0 o successiva. Se il client aggiorna o trasferisce la licenza a un altro client con versione 2.0.2 o successiva, i requisiti di funzionalità del dispositivo nella licenza verranno applicati, in quanto il client ora supporterà tale regola di utilizzo.

