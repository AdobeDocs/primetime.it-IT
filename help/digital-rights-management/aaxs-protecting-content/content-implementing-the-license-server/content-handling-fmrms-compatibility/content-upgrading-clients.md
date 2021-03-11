---
title: Aggiornamento dei client
description: Aggiornamento dei client
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '75'
ht-degree: 0%

---


# Aggiornamento dei client{#upgrading-clients}

Se un client FMRMS 1.x contatta un server di accesso Adobe, il server deve richiedere al client di eseguire l&#39;aggiornamento.

* La classe del gestore delle richieste è `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1RequestHandler`.
* L&#39;URL della richiesta è &quot;*URL di base da 1.x content*&quot; + &quot;/edcws/services/urn:EDCLicenseService&quot;

   A differenza di altri gestori di richieste di accesso Adobe, questo gestore non fornisce accesso ad alcuna informazione di richiesta o richiede l&#39;impostazione di dati di risposta. Crea un&#39;istanza del `FMRMSv1RequestHandler`, quindi chiama `close()`