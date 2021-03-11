---
title: Panoramica
description: Panoramica
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---


# Panoramica {#overview}

Per ottenere una licenza, i client formano una richiesta dai metadati incorporati nel contenuto in pacchetto, quindi inviano la richiesta al server licenze. Il server licenze utilizza le informazioni estratte dai metadati del contenuto per generare una licenza.

Se client e server supportano entrambi il protocollo versione 5, l’URL della richiesta è &quot;URL del server licenze nei metadati&quot; + &quot; [!DNL /flashaccess/license/v4]&quot;. Se il protocollo versione 3 è il massimo supportato dal client o dal server, i client DRM di Primetime inviano le richieste di autenticazione a &quot;URL del server licenze nei metadati&quot; + &quot; [!DNL /flashaccess/license/v3]&quot;. In caso contrario, le richieste di autenticazione vengono inviate a &quot;URL server licenze nei metadati&quot; + &quot; [!DNL /flashaccess/license/v1]&quot;

Un dispositivo può avere più licenze per lo stesso contenuto (stesso ID licenza), ma può avere una sola licenza per un particolare ID licenza e ID criterio DRM. Se riceve una licenza con un LicenseID/PolicyID duplicato, la nuova licenza sostituisce quella precedente solo se la data di rilascio della nuova licenza è successiva alla data di rilascio della licenza esistente. Questa logica viene utilizzata per elaborare le licenze incorporate nel contenuto. Pertanto, si sconsiglia di incorporare più di una licenza con lo stesso ID criterio DRM in un blocco di contenuto. La stessa logica si applica alle licenze passate al client tramite l’ API `DRMManager.storeVoucher()` ActionScript3; se il cliente dispone già di una licenza con una data di rilascio successiva, la licenza fornita potrebbe essere ignorata.

## Classi di gestione delle richieste di licenza {#section_190E3BEF316C4B09ACC21E4C2BAC5C75}

* `com.adobe.flashaccess.sdk.protocol.license.LicenseHandler` - Classe del gestore della richiesta di licenza. Legge e analizza le richieste di licenza. Il relativo metodo `getRequests()` restituisce un elenco di oggetti `LicenseRequestMessage`.
* `com.adobe.flashaccess.sdk.protocol.license.LicenseRequestMessage` - Classe messaggio di richiesta. Il chiamante deve eseguire un&#39;iterazione attraverso l&#39;elenco `LicenseRequestMessage` restituito da `getRequests()` e per ogni richiesta generare una licenza o impostare un codice di errore. Invoca `LicenseRequestMessage.getContentInfo()` per ottenere informazioni estratte dai metadati del contenuto, inclusi l&#39;ID del contenuto, l&#39;ID della licenza e i criteri DRM.

Le licenze e gli errori vengono inviati contemporaneamente alla chiamata del metodo `LicenseHandler.close()` .

Per ulteriori informazioni, consulta la [documentazione di riferimento API del server DRM](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/overview-summary.html) .
