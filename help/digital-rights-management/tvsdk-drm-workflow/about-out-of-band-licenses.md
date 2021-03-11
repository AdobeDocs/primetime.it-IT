---
title: Panoramica delle licenze fuori banda
description: Panoramica delle licenze fuori banda
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 0%

---


# Licenze fuori banda {#out-of-band-licenses}

È inoltre possibile ottenere licenze fuori banda (senza contattare un server di licenze DRM di Primetime) memorizzando la licenza su disco e in memoria utilizzando il metodo `storeVoucher()`.

Per riprodurre video crittografati in Primetime, il rispettivo runtime deve ottenere la licenza per quel video. La licenza contiene la chiave di decrittografia del video ed è generata dal server di licenza DRM di Primetime che il cliente ha implementato.

In genere, il runtime ottiene questa licenza inviando una richiesta di licenza al server licenze DRM di Primetime indicato nei metadati DRM del video ( `DRMContentData` class). L&#39;applicazione può attivare questa richiesta di licenza chiamando il metodo `DRMManager.loadVoucher()` .

`DRMManager.storeVoucher()` consente alla domanda di inviare le licenze ottenute fuori banda. Il runtime può quindi saltare il processo di richiesta della licenza e utilizzare le licenze inoltrate per la riproduzione di video crittografati. La licenza deve ancora essere generata dal server di licenza DRM Primetime prima che possa essere ottenuta fuori banda. Tuttavia, hai la possibilità di ospitare le licenze su qualsiasi server HTTP, invece di un server di licenza DRM di Primetime.

`DRMManager.storeVoucher()` viene utilizzato anche per supportare la condivisione di licenze tra più dispositivi. Dopo Primetime DRM 3.0, questa funzione è indicata come &quot;Supporto del dominio del dispositivo&quot;. Se la distribuzione supporta questo caso d&#39;uso, è possibile registrare più computer in un gruppo di dispositivi utilizzando il metodo `DRMManager.addToDeviceGroup()` . Se esiste un computer con una licenza valida associata a un dominio per un determinato contenuto, l&#39;applicazione può quindi estrarre la licenza serializzata utilizzando il metodo `DRMVoucher.toByteArray()` e sugli altri computer è possibile importare le licenze utilizzando il metodo `DRMManager.storeVoucher()` .

## Informazioni sulla registrazione dei dispositivi {#about-device-registration}

Tutte le licenze DRM di Primetime, al momento della creazione, devono essere associate a un&#39;entità finale. Il binding è il processo di crittografia che consente a una specifica entità di utilizzare la licenza solo per consentire a questa di utilizzare la licenza. Ciò è necessario per evitare &quot;licenze galleggianti&quot; che possono essere utilizzate da qualsiasi dispositivo arbitrario. Affinché le licenze DRM di Primetime siano &quot;pre-generate&quot;, significa che l&#39;obiettivo di queste licenze pregenerate deve essere noto in anticipo. Primetime DRM fa riferimento a questo come &quot;Registrazione del dispositivo&quot;.

## Registrare un dispositivo {#register-a-device}

Supponiamo che tu abbia eseguito le seguenti attività:

* Hai impostato l&#39;SDK del server DRM di Primetime.
* È stato configurato un server HTTP per il rilascio di licenze pregenerate.
* È stata creata un&#39;applicazione Primetime per visualizzare il contenuto protetto.

 La fase di registrazione del dispositivo prevede le seguenti azioni:

1. L&#39;applicazione crea un ID generato in modo casuale.
1. L&#39;applicazione richiama il metodo `DRMManager.authenticate()` . L’applicazione deve includere l’ID generato in modo casuale nella richiesta di autenticazione. Ad esempio, includi l’ID nel campo del nome utente.
1. L&#39;azione indicata nel passaggio 2 comporterà l&#39;invio da parte di DRM di Primetime di una richiesta di autenticazione al server del cliente. Questa richiesta include il certificato del dispositivo:
   1. Il server estrae il certificato del dispositivo e l’ID generato dalla richiesta e archivia.
   1. Il sottosistema del cliente genera in anticipo le licenze per questo certificato dispositivo, le memorizza e le concede l’accesso in modo da associarle all’ID generato. .
1. Il server risponde alla richiesta con un messaggio &quot;success&quot;.
1. L&#39;applicazione memorizza l&#39;ID generato.

Dopo la registrazione del dispositivo, l&#39;applicazione utilizza l&#39;ID generato nello stesso modo in cui avrebbe usato l&#39;ID dispositivo nello schema precedente:
1. L&#39;applicazione cercherà di individuare l&#39;ID generato.
1. Se viene trovato l’ID generato, l’applicazione utilizza l’ID generato durante il download delle licenze pregenerate. L&#39;applicazione invierà le licenze al client DRM Primetime per l&#39;utilizzo utilizzando il metodo `DRMManager.storeVoucher()` . .
1. Se l&#39;ID generato non viene trovato, l&#39;applicazione passerà attraverso la procedura di registrazione del dispositivo.

## Ripristino della fabbrica DRM {#drm-factory-reset}

Quando l&#39;utente del dispositivo richiama l&#39;opzione di reimpostazione della fabbrica DRM, il certificato del dispositivo verrà eliminato. Per continuare a riprodurre il contenuto protetto, l&#39;applicazione deve seguire nuovamente la procedura di registrazione del dispositivo. Se l’applicazione invia una licenza pre-generata obsoleta, il client DRM di Primetime la rifiuterà poiché la licenza è stata crittografata per un ID dispositivo precedente.

* API Flash: [DRMManager.resetDRMVouchers()](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/net/drm/DRMManager.html#resetDRMVouchers()) - (Può essere chiamato solo in risposta a determinati codici di errore DRM non recuperabili).
* API iOS: [DRMManager resetDRM](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a0dd6c9662428583196e0419d3ea69446)
* API Android: [DRMManager.resetDRM()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#resetDRM(com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMOperationCompleteCallback))