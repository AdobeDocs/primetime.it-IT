---
seo-title: Aggiornamento dei client
title: Aggiornamento dei client
uuid: 9c9bc7da-2a97-4659-945a-554d778d30a3
translation-type: tm+mt
source-git-commit: 5cf90a75d8805fb64d7d145722ad10a1ce77a14d

---


# Aggiornamento dei client{#upgrading-clients}

Se un client FMRMS 1.x contatta un server Adobe Access, il server deve richiedere al client di eseguire l&#39;aggiornamento.

* La classe gestore di richieste è `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1RequestHandler`.
* L’URL della richiesta è &quot;URL di *base dal contenuto* 1.x&quot; + &quot;/edcws/services/urn:EDCLicenseService&quot;

   A differenza di altri gestori di richieste di Adobe Access, questo gestore non fornisce l&#39;accesso ad alcuna informazione di richiesta né richiede l&#39;impostazione di dati di risposta. Crea un’istanza del `FMRMSv1RequestHandler`, quindi chiama `close()`