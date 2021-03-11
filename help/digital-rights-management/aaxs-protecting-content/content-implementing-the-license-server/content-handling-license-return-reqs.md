---
title: Gestione delle richieste di restituzione delle licenze
description: Gestione delle richieste di restituzione delle licenze
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---


# Gestione delle richieste di restituzione delle licenze{#handling-license-return-requests}

Se l’applicazione client deve restituire una licenza, richiama l’API ActionScript DRMManager.returnVoucher() per avviare il processo. Questa API può funzionare in modalità immediateCommit o in modalità confirmFirst. Se immediateCommit è impostato su true, il client eliminerà immediatamente le licenze locali, senza attendere la conferma da parte del server licenze di aver ricevuto la richiesta di restituzione delle licenze. Il server licenze di Adobe Access deve elaborare la richiesta e inviare una risposta al client. Il fatto che il server licenze esegua o meno la richiesta (ad esempio, decrementare il conteggio delle licenze per l&#39;utente specificato) dipende dal server licenze da decidere.

* La classe del gestore delle richieste è com.adobe.flashaccess.sdk.protocol.licenziereturn.LicenseReturnHandler
* La classe del messaggio di richiesta è com.adobe.flashaccess.sdk.protocol.licenziereturn.LicenseReturnRequestMessage

La versione minima richiesta dell&#39;SDK di accesso Adobe è la versione 5; l’URL della richiesta sarà &quot; `/flashaccess/lreturn/v5`&quot;. Come per la cancellazione del dominio, il server deve utilizzare `getRequestPhase()` per determinare se il client sta visualizzando l’anteprima della restituzione della licenza.
