---
seo-title: Versione minima client
title: Versione minima client
uuid: 9f39e4e7-64eb-43ea-b194-b744838a411e
translation-type: tm+mt
source-git-commit: 53654b740b03c6a79394d30704a41186d4655237

---


# Versione minima client {#minimum-client-version}

Adobe Access 2.0.2 e versioni successive introducono alcune nuove regole di utilizzo, che non sono comprese dai client Adobe Access 2.0. Impostando la versione client minima supportata ( `HandlerConfiguration.setMinSupportedClientVersion()`), il server licenze può controllare il comportamento dei client meno recenti quando incontrano licenze con queste regole di utilizzo. In base a questa impostazione, il server può indicare se i client meno recenti possono ignorare le regole di utilizzo che non conoscono o se i client meno recenti non saranno in grado di utilizzare licenze con tali regole di utilizzo.

Ad esempio:

* Se la licenza specifica i requisiti di capacità del dispositivo (capacità del [dispositivo necessarie per riprodurre contenuto](../../../aaxs-protecting-content/content-introduction/content-usage-rules/content-runtime-application-restrictions/content-device-capabilities.md)protetto), i client Adobe Access 2.0.2 e versioni successive possono applicare tali requisiti.
* Se il server licenze non desidera che il contenuto venga riprodotto su client che non conoscono i requisiti di funzionalità del dispositivo, impostare la versione client minima supportata su 2 (per la versione 2.0.2). Ciò impedirà al server di rilasciare licenze ai client Adobe Access prima della 2.0.2. La versione client minima verrà applicata anche se la licenza viene trasferita da un client all&#39;altro.
* Se il server licenze desidera consentire ai client meno recenti di ignorare i requisiti di funzionalità del dispositivo, impostare la versione client minima supportata su 1 (per Adobe Access 2.0). Il server rilascerà una licenza per qualsiasi versione client 2.0 e successiva. Se il client aggiorna o trasferisce la licenza a un altro client con versione 2.0.2 o successiva, i requisiti di funzionalità del dispositivo nella licenza saranno applicati, poiché il client ora supporterà tale regola di utilizzo.

