---
title: Aggiornamento dei client
description: Aggiornamento dei client
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '75'
ht-degree: 0%

---

# Aggiornamento dei client{#upgrading-clients}

Se un client FMRMS 1.x contatta un Adobe server Access, il server deve richiedere al client di eseguire l&#39;aggiornamento.

* La classe del gestore richieste è `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1RequestHandler`.
* L’URL della richiesta è &quot;*URL di base da contenuto 1.x*&quot; + &quot;/edcws/services/urn:EDCLicenseService&quot;

  A differenza di altri gestori di richieste di accesso Adobe, questo gestore non fornisce l’accesso ad alcuna informazione di richiesta né richiede l’impostazione di dati di risposta. Crea un&#39;istanza di `FMRMSv1RequestHandler`, quindi chiama `close()`
