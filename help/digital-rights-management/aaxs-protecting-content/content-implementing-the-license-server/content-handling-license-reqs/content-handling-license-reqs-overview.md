---
title: Panoramica
description: Panoramica
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---

# Panoramica{#overview}

Per richiedere una licenza, il client invia i metadati incorporati nel contenuto durante la creazione del pacchetto. Il server licenze utilizza le informazioni contenute nei metadati del contenuto per generare una licenza.

Il `LicenseHandler` legge una richiesta di licenza e la analizza. `LicenseHandler`si estende `BatchHandlerBase` per soddisfare richieste di licenze in batch, sebbene questa funzione non sia attualmente supportata dai client Adobe Access. Il `getRequests()` il metodo restituirà un elenco di `LicenseRequestMessage` oggetti. Il chiamante deve eseguire l&#39;iterazione attraverso `LicenseRequestMessages`, e per ogni richiesta, genera una licenza o imposta un codice di errore (vedi `LicenseRequestMessage` documentazione di riferimento API). Per ogni richiesta di licenza, il server determina se emetterà una licenza. Chiamata `LicenseRequestMessage.getContentInfo()` per ottenere informazioni estratte dai metadati del contenuto, tra cui l’ID contenuto, l’ID licenza e i criteri.

* La classe del gestore richieste è `com.adobe.flashaccess.sdk.protocol.license.LicenseHandler`
* La classe del messaggio di richiesta è `com.adobe.flashaccess.sdk.protocol.license.LicenseRequestMessage`
* Se sia il client che il server supportano la versione 5 del protocollo, l&#39;URL della richiesta è &quot;License Server URL in metadata: + &quot;/flashaccess/license/v4&quot;. Se il protocollo versione 3 è il massimo supportato dal client o dal server, i client Adobe Access invieranno richieste di autenticazione a &quot;URL del server licenze nei metadati&quot; + &quot;/flashaccess/license/v3&quot;. In caso contrario, le richieste di autenticazione vengono inviate a &quot;URL del server licenze nei metadati&quot; + &quot;/flashaccess/license/v1&quot;

Se si verifica un errore durante l’analisi della richiesta, viene `HandlerParsingException` viene lanciato. Questa eccezione contiene informazioni sull&#39;errore da restituire al client. Per recuperare le informazioni sull’errore, chiama `HandlerParsingException.getErrorData()`. Se si verifica un errore durante la generazione di una licenza perché i requisiti dei criteri non sono stati soddisfatti, viene visualizzato un messaggio `PolicyEvaluationException` viene lanciato. Questa eccezione include anche `ErrorData` da restituire al client. Consulta la documentazione API per `LicenseRequestMessage.generateLicense()` per informazioni dettagliate su come vengono valutati i criteri durante la generazione della licenza.

Le licenze e gli errori vengono inviati contemporaneamente quando `LicenseHandler.close()` viene chiamato.

Un dispositivo può disporre di più licenze per lo stesso contenuto (stesso ID licenza), ma può disporre di una sola licenza per uno specifico ID licenza e ID criterio. Se viene ricevuta una licenza con un LicenseID/PolicyID duplicato, la nuova licenza sostituirà quella precedente solo se la data di rilascio della nuova licenza è successiva alla data di rilascio della licenza esistente. Questa logica viene utilizzata per elaborare le licenze incorporate nel contenuto. Pertanto, si sconsiglia di incorporare più di una licenza con lo stesso ID policy in un blocco di contenuto. La stessa logica si applica alle licenze passate al client tramite `DRMManager.storeVoucher()` API ActionScript 3; se il client dispone già di una licenza con una data di rilascio successiva, la licenza fornita potrebbe essere ignorata.
