---
seo-title: Aggiornamento dei client
title: Aggiornamento dei client
uuid: 9c9bc7da-2a97-4659-945a-554d778d30a3
translation-type: tm+mt
source-git-commit: 5cf90a75d8805fb64d7d145722ad10a1ce77a14d
workflow-type: tm+mt
source-wordcount: '75'
ht-degree: 0%

---


# Aggiornamento dei client{#upgrading-clients}

Se un client FMRMS 1.x contatta un server di accesso  Adobe, il server deve richiedere al client di eseguire l&#39;aggiornamento.

* La classe del gestore di richieste è `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1RequestHandler`.
* L&#39;URL della richiesta è &quot;*URL di base da 1.x content*&quot; + &quot;/edcws/services/urn:EDCLicenseService&quot;

   A differenza di altri gestori di richieste di accesso  Adobe, questo gestore non fornisce l&#39;accesso alle informazioni di richiesta né richiede l&#39;impostazione di dati di risposta. Creare un&#39;istanza del `FMRMSv1RequestHandler`, quindi chiamare `close()`