---
title: Versione client minima
description: Versione client minima
copied-description: true
exl-id: ba311d33-f3dd-42c5-ac66-7ad665d1bd20
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---

# Versione client minima {#minimum-client-version}

Adobe Access 2.0.2 e versioni successive introducono alcune nuove regole di utilizzo che non sono comprese dai client Adobe Access 2.0. Impostando la versione client minima supportata ( `HandlerConfiguration.setMinSupportedClientVersion()`), il server licenze può controllare il comportamento dei client meno recenti quando incontrano licenze con queste regole di utilizzo. In base a questa impostazione, il server può indicare se i client meno recenti possono ignorare le regole di utilizzo che non conoscono o se i client meno recenti non possono utilizzare le licenze con tali regole di utilizzo.

Ad esempio:

* Se la licenza specifica i requisiti di funzionalità del dispositivo ( [Funzionalità del dispositivo necessarie per riprodurre contenuti protetti](../../../aaxs-protecting-content/content-introduction/content-usage-rules/content-runtime-application-restrictions/content-device-capabilities.md)), Adobe Access Client 2.0.2 e versioni successive possono applicare tali requisiti.
* Se il server licenze non desidera che il contenuto venga riprodotto su client che non soddisfano i requisiti di funzionalità del dispositivo, impostare la versione client minima supportata su 2 (per 2.0.2). Questo impedirà al server di rilasciare licenze ai client di Access Adobe prima della versione 2.0.2. La versione minima del client verrà applicata anche se la licenza viene trasferita da un client a un altro.
* Se il server licenze desidera consentire ai client meno recenti di ignorare i requisiti di funzionalità del dispositivo, impostare la versione minima del client supportato su 1 (ad Adobe Access 2.0). Il server rilascerà una licenza a qualsiasi client versione 2.0 o successiva. Se il client aggiorna o trasferisce la licenza a un altro client con versione 2.0.2 o successiva, verranno applicati i requisiti di funzionalità del dispositivo nella licenza, in quanto il client ora supporta tale regola di utilizzo.
