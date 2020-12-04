---
seo-title: Panoramica
title: Panoramica
uuid: d3bfa65b-2360-4843-b59e-71451fa62a2c
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---


# Overview{#overview}

Per richiedere una licenza, il client invia i metadati incorporati nel contenuto durante la creazione del pacchetto. Il server licenze utilizza le informazioni contenute nei metadati del contenuto per generare una licenza.

La `LicenseHandler` legge una richiesta di licenza e analizza la richiesta. `LicenseHandler`si estende  `BatchHandlerBase` per soddisfare le richieste di licenza batch, anche se al momento questa funzione non è supportata dai client di accesso  Adobe. Il metodo `getRequests()` restituirà un Elenco di oggetti `LicenseRequestMessage`. Il chiamante deve eseguire un&#39;iterazione attraverso la `LicenseRequestMessages` e per ogni richiesta, generare una licenza o impostare un codice di errore (per informazioni dettagliate, consultate la documentazione di riferimento API `LicenseRequestMessage`). Per ogni richiesta di licenza, il server determina se rilascerà o meno una licenza. Chiamate `LicenseRequestMessage.getContentInfo()` per ottenere informazioni estratte dai metadati del contenuto, inclusi ID contenuto, ID licenza e criteri.

* La classe del gestore di richieste è `com.adobe.flashaccess.sdk.protocol.license.LicenseHandler`
* La classe del messaggio di richiesta è `com.adobe.flashaccess.sdk.protocol.license.LicenseRequestMessage`
* Se client e server supportano entrambi il protocollo versione 5, l’URL della richiesta è &quot;URL server licenze nei metadati: + &quot;/flashaccess/license/v4&quot;. Se il protocollo versione 3 è il massimo supportato dal client o dal server,  client Accesso Adobe invieranno le richieste di autenticazione a &quot;URL del server delle licenze nei metadati&quot; + &quot;/flashaccess/license/v3&quot;. In caso contrario, le richieste di autenticazione vengono inviate a &quot;URL del server delle licenze nei metadati&quot; + &quot;/flashaccess/license/v1&quot;

Se si verifica un errore durante l&#39;analisi della richiesta, viene restituito un `HandlerParsingException`. Questa eccezione contiene informazioni sull&#39;errore da restituire al client. Per recuperare le informazioni sull&#39;errore, chiamare `HandlerParsingException.getErrorData()`. Se si verifica un errore durante la generazione di una licenza perché i requisiti dei criteri non sono stati soddisfatti, viene restituito un `PolicyEvaluationException`. Questa eccezione include anche `ErrorData` da restituire al client. Per informazioni dettagliate su come valutare i criteri durante la generazione della licenza, consultate la documentazione API per `LicenseRequestMessage.generateLicense()`.

Le licenze e gli errori vengono inviati contemporaneamente quando si chiama `LicenseHandler.close()`.

Un dispositivo può avere più licenze per lo stesso contenuto (stesso ID licenza), ma può avere una sola licenza per un ID licenza e un ID criterio specifici. Se riceve una licenza con un ID licenza/PolicyID duplicato, la nuova licenza sostituirà quella precedente solo se la data di rilascio della nuova licenza è successiva alla data di rilascio della licenza esistente. Questa logica viene utilizzata per elaborare le licenze incorporate nel contenuto, pertanto non è consigliabile incorporare più licenze con lo stesso ID criterio in una parte di contenuto. La stessa logica si applica alle licenze passate al client tramite l&#39;API `DRMManager.storeVoucher()`  ActionScript3; se il cliente possiede già una licenza con una data di rilascio successiva, la licenza fornita potrebbe essere ignorata.
