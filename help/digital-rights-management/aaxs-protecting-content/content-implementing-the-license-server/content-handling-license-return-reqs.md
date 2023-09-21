---
title: Gestione delle richieste di restituzione delle licenze
description: Gestione delle richieste di restituzione delle licenze
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# Gestione delle richieste di restituzione delle licenze{#handling-license-return-requests}

Se l&#39;applicazione client deve restituire una licenza, richiama l&#39;API Actionscript DRMManager.returnVoucher() per avviare il processo. Questa API può funzionare in modalità immediateCommit o confirmFirst. Se immediateCommit è impostato su true, il client eliminerà immediatamente le licenze locali senza attendere la conferma da parte del server licenze che ha ricevuto la richiesta di restituire le licenze. Il server licenze di accesso Adobe deve elaborare la richiesta e inviare una risposta al client. Spetta al server licenze decidere se il server licenze esegue effettivamente o meno operazioni con la richiesta (ad esempio decrementare il numero di licenze per l’utente specificato).

* La classe del gestore richieste è com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnHandler
* La classe del messaggio di richiesta è com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnRequestMessage

La versione SDK minima per l’accesso agli Adobi richiesta è la versione 5; l’URL della richiesta sarà &quot; `/flashaccess/lreturn/v5`&quot;. Come per la cancellazione del dominio, il server deve utilizzare `getRequestPhase()` per determinare se il client sta visualizzando l&#39;anteprima di una licenza.
