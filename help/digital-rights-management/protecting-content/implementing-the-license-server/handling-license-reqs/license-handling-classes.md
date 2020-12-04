---
seo-title: Panoramica
title: Panoramica
uuid: 2bbf0aa1-df35-429d-84df-db357fa53e47
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---


# Panoramica {#overview}

Per ottenere una licenza, i client formano una richiesta dai metadati incorporati nel contenuto del pacchetto, quindi inviano la richiesta al server della licenza. Il server licenze utilizza le informazioni estratte dai metadati del contenuto per generare una licenza.

Se client e server supportano entrambi il protocollo versione 5, l&#39;URL della richiesta è &quot;URL del server delle licenze nei metadati&quot; + &quot; [!DNL /flashaccess/license/v4]&quot;. Se il protocollo versione 3 è il massimo supportato dal client o dal server, i client DRM Primetime inviano quindi le richieste di autenticazione a &quot;URL del server delle licenze nei metadati&quot; + &quot; [!DNL /flashaccess/license/v3]&quot;. In caso contrario, le richieste di autenticazione vengono inviate a &quot;URL del server delle licenze nei metadati&quot; + &quot; [!DNL /flashaccess/license/v1]&quot;

Un dispositivo può avere più licenze per lo stesso contenuto (stesso ID licenza), ma può avere una sola licenza per un ID licenza particolare e un ID criterio DRM. Se riceve una licenza con un ID licenza/PolicyID duplicato, la nuova licenza sostituisce la precedente solo se la data di rilascio della nuova licenza è successiva alla data di rilascio della licenza esistente. Questa logica viene utilizzata per elaborare le licenze incorporate nel contenuto. Pertanto, non è consigliabile incorporare più licenze con lo stesso ID criterio DRM in una parte di contenuto. La stessa logica si applica alle licenze passate al client tramite l&#39;API `DRMManager.storeVoucher()`  ActionScript3; se il cliente possiede già una licenza con una data di rilascio successiva, la licenza fornita potrebbe essere ignorata.

## Classi di gestione delle richieste di licenza {#section_190E3BEF316C4B09ACC21E4C2BAC5C75}

* `com.adobe.flashaccess.sdk.protocol.license.LicenseHandler` - Questa è la classe del gestore di richieste di licenza. Legge e analizza le richieste di licenza. Il relativo metodo `getRequests()` restituisce un elenco di oggetti `LicenseRequestMessage`.
* `com.adobe.flashaccess.sdk.protocol.license.LicenseRequestMessage` - Questa è la classe del messaggio di richiesta. Il chiamante deve iterare nell&#39;elenco `LicenseRequestMessage` restituito da `getRequests()` e per ogni richiesta generare una licenza o impostare un codice di errore. Chiamate `LicenseRequestMessage.getContentInfo()` per ottenere informazioni estratte dai metadati del contenuto, inclusi ID contenuto, ID licenza e criteri DRM.

Licenze ed errori vengono inviati contemporaneamente quando viene chiamato il metodo `LicenseHandler.close()`.

Per ulteriori informazioni, consultate la [documentazione di riferimento per l&#39;API del server DRM](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/overview-summary.html).
