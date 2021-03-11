---
title: Gestire le richieste di restituzione delle licenze
description: Gestire le richieste di restituzione delle licenze
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---


# Gestire le richieste di restituzione delle licenze{#handle-license-return-requests}

Se l’applicazione client deve restituire una licenza, richiama l’ API `DRMManager.returnVoucher()` Actionscript per avviare il processo. Questa API può funzionare in modalità `immediateCommit` o `confirmFirst`. Se `immediateCommit` è impostato su `true`, il client elimina immediatamente le licenze locali senza attendere la conferma dal server licenze di aver ricevuto la richiesta di restituzione delle licenze. Il server di licenza Adobe Primetime DRM deve elaborare la richiesta e inviare una risposta al client. Il server licenze decide se il server licenze elabora o meno la richiesta, ad esempio ridurre il numero di licenze per un utente specificato.

* La classe del gestore richieste è `com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnHandler`
* La classe del messaggio di richiesta è `com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnRequestMessage`

La versione minima `Adobe Primetime DRM` SDK richiesta è la versione 5; l&#39;URL della richiesta è &quot; [!DNL /flashaccess/lreturn/v5]&quot;. Come per la cancellazione del dominio, il server utilizza `getRequestPhase()` per determinare se il client può visualizzare in anteprima la restituzione di una licenza.
