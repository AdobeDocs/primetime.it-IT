---
title: Panoramica
description: Panoramica
copied-description: true
exl-id: 267188d0-83f8-42dc-88e3-78b52945cb6c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---

# Panoramica {#overview}

Per ottenere una licenza, i client formano una richiesta dai metadati incorporati nel contenuto del pacchetto, quindi inviano tale richiesta al server licenze. Per generare una licenza, il server licenze utilizza le informazioni estratte dai metadati del contenuto.

Se il client e il server supportano entrambi la versione 5 del protocollo, l&#39;URL della richiesta sarà &quot;License Server URL in metadata&quot; + &quot; [!DNL /flashaccess/license/v4]&quot;. Se il protocollo versione 3 è il massimo supportato dal client o dal server, i client DRM di Primetime inviano richieste di autenticazione a &quot;URL server licenze nei metadati&quot; + &quot; [!DNL /flashaccess/license/v3]&quot;. In caso contrario, le richieste di autenticazione vengono inviate a &quot;URL del server licenze nei metadati&quot; + &quot; [!DNL /flashaccess/license/v1]&quot;

Un dispositivo può disporre di più licenze per lo stesso contenuto (stesso ID licenza), ma può disporre di una sola licenza per un determinato ID licenza e ID criteri DRM. Se viene ricevuta una licenza con un LicenseID/PolicyID duplicato, la nuova licenza sostituirà quella precedente solo se la data di rilascio della nuova licenza è successiva alla data di rilascio della licenza esistente. Questa logica viene utilizzata per elaborare le licenze incorporate nel contenuto. Pertanto, non è consigliabile incorporare più di una licenza con lo stesso ID di criteri DRM in un blocco di contenuto. La stessa logica si applica alle licenze passate al client tramite `DRMManager.storeVoucher()` API ActionScript 3; se il client dispone già di una licenza con una data di rilascio successiva, la licenza fornita potrebbe essere ignorata.

## Classi di gestione richieste di licenza {#section_190E3BEF316C4B09ACC21E4C2BAC5C75}

* `com.adobe.flashaccess.sdk.protocol.license.LicenseHandler` - Questa è la classe del gestore di richieste di licenza. Legge ed analizza le richieste di licenza. I suoi `getRequests()` il metodo restituisce un elenco di `LicenseRequestMessage` oggetti.
* `com.adobe.flashaccess.sdk.protocol.license.LicenseRequestMessage` - Questa è la classe del messaggio di richiesta. Il chiamante deve eseguire l&#39;iterazione attraverso `LicenseRequestMessage` elenco restituito da `getRequests()`, e per ogni richiesta genera una licenza o imposta un codice di errore. Chiamata `LicenseRequestMessage.getContentInfo()` per ottenere informazioni estratte dai metadati del contenuto, inclusi ID contenuto, ID licenza e criteri DRM.

Le licenze e gli errori vengono inviati contemporaneamente quando `LicenseHandler.close()` viene chiamato il metodo.

Consulta la [Documentazione di riferimento sulle API del server DRM](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/overview-summary.html) per i dettagli.
