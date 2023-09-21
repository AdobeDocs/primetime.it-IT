---
title: Gestire le richieste di restituzione delle licenze
description: Gestire le richieste di restituzione delle licenze
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---

# Gestire le richieste di restituzione delle licenze{#handle-license-return-requests}

Se l&#39;applicazione client deve restituire una licenza, richiama `DRMManager.returnVoucher()` API Actionscript per avviare il processo. Questa API può funzionare in un `immediateCommit` modalità o un `confirmFirst` modalità. Se `immediateCommit` è impostato su `true`, il client elimina immediatamente le licenze locali senza attendere la conferma da parte del server licenze che ha ricevuto la richiesta di restituire le licenze. Il server licenze Adobe Primetime DRM deve elaborare la richiesta e inviare una risposta al client. Il server licenze decide se elaborare o meno la richiesta, ad esempio decrementare il numero di licenze per un utente specificato.

* La classe del gestore richieste è `com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnHandler`
* La classe del messaggio di richiesta è `com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnRequestMessage`

Il minimo `Adobe Primetime DRM` La versione dell’SDK richiesta è la versione 5; l’URL della richiesta è &quot; [!DNL /flashaccess/lreturn/v5]&quot;. Come per la cancellazione del dominio, il server utilizza `getRequestPhase()` per determinare se il client può visualizzare in anteprima una licenza restituita.
