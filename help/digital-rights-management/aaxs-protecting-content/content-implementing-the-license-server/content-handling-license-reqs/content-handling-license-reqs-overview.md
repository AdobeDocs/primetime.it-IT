---
title: Panoramica
description: Panoramica
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---


# Panoramica{#overview}

Per richiedere una licenza, il client invia i metadati incorporati nel contenuto durante la creazione del pacchetto. Il server licenze utilizza le informazioni nei metadati del contenuto per generare una licenza.

Il `LicenseHandler` legge una richiesta di licenza e analizza la richiesta. `LicenseHandler`si estende  `BatchHandlerBase` per soddisfare le richieste di licenze batch, anche se questa funzione non è attualmente supportata dai client di Adobe Access. Il metodo `getRequests()` restituirà un Elenco di oggetti `LicenseRequestMessage`. Il chiamante deve eseguire un&#39;iterazione attraverso `LicenseRequestMessages` e per ogni richiesta, generare una licenza o impostare un codice di errore (per ulteriori informazioni, consulta la documentazione di riferimento API `LicenseRequestMessage` ). Per ogni richiesta di licenza, il server determina se rilascerà una licenza. Chiama `LicenseRequestMessage.getContentInfo()` per ottenere informazioni estratte dai metadati del contenuto, inclusi l’ID del contenuto, l’ID della licenza e i criteri.

* La classe del gestore richieste è `com.adobe.flashaccess.sdk.protocol.license.LicenseHandler`
* La classe del messaggio di richiesta è `com.adobe.flashaccess.sdk.protocol.license.LicenseRequestMessage`
* Se il protocollo di supporto client e server versione 5, l’URL della richiesta è &quot;URL del server licenze nei metadati: + &quot;/flashaccess/license/v4&quot;. Se il protocollo versione 3 è il massimo supportato dal client o dal server, i client di Adobe Access invieranno richieste di autenticazione a &quot;URL del server licenze nei metadati&quot; + &quot;/flashaccess/license/v3&quot;. In caso contrario, le richieste di autenticazione vengono inviate a &quot;URL server licenze nei metadati&quot; + &quot;/flashaccess/license/v1&quot;

Se si verifica un errore durante l’analisi della richiesta, viene generato un `HandlerParsingException`. Questa eccezione contiene informazioni di errore da restituire al client. Per recuperare le informazioni sull’errore, chiama `HandlerParsingException.getErrorData()`. Se durante la generazione di una licenza si verifica un errore perché i requisiti dei criteri non sono stati soddisfatti, viene lanciato un `PolicyEvaluationException`. Questa eccezione include anche `ErrorData` da restituire al client. Per informazioni dettagliate su come valutare i criteri durante la generazione delle licenze, consulta la documentazione API per `LicenseRequestMessage.generateLicense()` .

Le licenze e gli errori vengono inviati contemporaneamente alla chiamata di `LicenseHandler.close()`.

Un dispositivo può avere più licenze per lo stesso contenuto (stesso ID licenza), ma può avere una sola licenza per un particolare ID licenza e ID criterio. Se riceve una licenza con un LicenseID/PolicyID duplicato, la nuova licenza sostituirà quella precedente solo se la data di rilascio della nuova licenza è successiva alla data di rilascio della licenza esistente. Questa logica viene utilizzata per elaborare le licenze incorporate nel contenuto, pertanto si sconsiglia di incorporare più di una licenza con lo stesso ID criterio in un blocco di contenuto. La stessa logica si applica alle licenze passate al client tramite l’ API `DRMManager.storeVoucher()` ActionScript3; se il cliente dispone già di una licenza con una data di rilascio successiva, la licenza fornita potrebbe essere ignorata.
