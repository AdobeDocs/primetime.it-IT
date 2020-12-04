---
seo-title: Gestione delle richieste di restituzione delle licenze
title: Gestione delle richieste di restituzione delle licenze
uuid: 994df5af-476a-4ee8-b371-8900241be83d
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---


# Gestire le richieste di restituzione delle licenze{#handle-license-return-requests}

Se l&#39;applicazione client deve restituire una licenza, richiama l&#39;API `DRMManager.returnVoucher()` Actionscript per avviare il processo. Questa API può funzionare in modalità `immediateCommit` o `confirmFirst`. Se `immediateCommit` è impostato su `true`, il client elimina immediatamente le licenze locali senza attendere la conferma dal server licenze di aver ricevuto la richiesta di restituzione delle licenze. Il server licenze Adobe Primetime DRM  deve elaborare la richiesta e inviare una risposta al client. Il server licenze elabora o meno la richiesta, ad esempio decrementare il numero di licenze per un utente specificato, viene deciso dal server licenze.

* La classe del gestore di richieste è `com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnHandler`
* La classe del messaggio di richiesta è `com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnRequestMessage`

La versione minima `Adobe Primetime DRM` dell&#39;SDK richiesta è la versione 5; l&#39;URL della richiesta è &quot; [!DNL /flashaccess/lreturn/v5]&quot;. Come per la deregistrazione del dominio, il server utilizza `getRequestPhase()` per determinare se il client può visualizzare l&#39;anteprima di una restituzione di licenza.
