---
seo-title: Gestione delle richieste di restituzione delle licenze
title: Gestione delle richieste di restituzione delle licenze
uuid: d184faea-88cb-44f3-a253-e5314d577f17
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---


# Gestione delle richieste di restituzione licenze{#handling-license-return-requests}

Se l&#39;applicazione client deve restituire una licenza, richiama l&#39;API ActionScript DRMManager.returnVoucher() per avviare il processo. Questa API può funzionare in modalità immediateCommit o in modalità ConfirmFirst. Se immediateCommit è impostato su true, il client eliminerà immediatamente le licenze locali, senza attendere la conferma dal server licenze di aver ricevuto la richiesta di restituzione delle licenze. Il server licenze di accesso al Adobe  deve elaborare la richiesta e inviare una risposta al client. Il fatto che il server licenze esegua o meno le operazioni con la richiesta (ad esempio, decremento di un numero di licenze per l&#39;utente specificato) dipende dalle decisioni del server licenze.

* La classe del gestore di richieste è com.adobe.flashaccess.sdk.protocol.licenziereturn.LicenseReturnHandler
* La classe del messaggio di richiesta è com.adobe.flashaccess.sdk.protocol.licenziereturn.LicenseReturnRequestMessage

La versione minima dell&#39;SDK per l&#39;accesso ai Adobi richiesta è la versione 5; l&#39;URL della richiesta sarà &quot; `/flashaccess/lreturn/v5`&quot;. Come per la deregistrazione del dominio, il server deve utilizzare `getRequestPhase()` per determinare se il client sta visualizzando l&#39;anteprima di una restituzione della licenza.
