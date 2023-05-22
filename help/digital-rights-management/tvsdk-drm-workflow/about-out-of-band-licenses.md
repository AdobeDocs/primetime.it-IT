---
title: Panoramica delle licenze fuori banda
description: Panoramica delle licenze fuori banda
copied-description: true
exl-id: 31a9f097-74e8-41d0-9b9a-1c2a08d3e63a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 0%

---

# Licenze out-of-band {#out-of-band-licenses}

Le licenze possono anche essere ottenute fuori banda (senza contattare un server di licenze DRM Primetime) memorizzando la licenza su disco e in memoria utilizzando `storeVoucher()` metodo.

Per riprodurre video crittografati in Primetime, il rispettivo runtime deve ottenere la licenza per tale video. La licenza contiene la chiave di decrittografia del video ed è generata dal server licenze DRM Primetime distribuito dal cliente.

Il runtime generalmente ottiene questa licenza inviando una richiesta di licenza al server di licenze DRM Primetime indicato nei metadati DRM del video ( `DRMContentData` classe). L’applicazione può attivare questa richiesta di licenza chiamando il `DRMManager.loadVoucher()` metodo.

`DRMManager.storeVoucher()` consente all&#39;applicazione di inviare le licenze ottenute fuori banda. Il runtime può quindi ignorare il processo di richiesta della licenza e utilizzare le licenze inoltrate per la riproduzione di video crittografati. Prima di poter essere ottenuta fuori banda, la licenza deve ancora essere generata dal server di licenze DRM Primetime. Tuttavia, è possibile scegliere di ospitare le licenze su qualsiasi server HTTP, anziché su un server di licenze DRM Primetime.

`DRMManager.storeVoucher()` viene utilizzato anche per supportare la condivisione delle licenze tra più dispositivi. Dopo Primetime DRM 3.0, questa funzione viene definita &quot;Supporto del dominio del dispositivo&quot;. Se la distribuzione supporta questo caso d’uso, puoi registrare più computer in un gruppo di dispositivi utilizzando `DRMManager.addToDeviceGroup()` metodo. Se è presente un computer con una licenza valida associata al dominio per un determinato contenuto, l&#39;applicazione può quindi estrarre la licenza serializzata utilizzando `DRMVoucher.toByteArray()` e sugli altri computer è possibile importare le licenze utilizzando il `DRMManager.storeVoucher()` metodo.

## Informazioni sulla registrazione del dispositivo {#about-device-registration}

Tutte le licenze DRM di Primetime, al momento della creazione, devono essere associate a un’entità finale. Il binding è il processo di crittografia che consente a una specifica entità di utilizzare la licenza. Ciò è necessario per evitare &quot;licenze flottanti&quot; che possono essere utilizzate da qualsiasi dispositivo arbitrario. Affinché Primetime DRM possa &quot;pre-generare&quot; licenze, il &quot;target&quot; di queste licenze pregenerate deve essere noto in anticipo. Primetime DRM si riferisce a questo come &quot;Registrazione del dispositivo&quot;.

## Registrare un dispositivo {#register-a-device}

Supponiamo che tu abbia eseguito le seguenti attività:

* È stato configurato l’SDK del server DRM Primetime.
* È stato configurato un server HTTP per l&#39;emissione di licenze pregenerate.
* Hai creato un’applicazione Primetime per visualizzare il contenuto protetto.

 La fase di registrazione del dispositivo prevede le seguenti azioni:

1. L’applicazione crea un ID generato in modo casuale.
1. L&#39;applicazione richiama `DRMManager.authenticate()` metodo. L’applicazione deve includere l’ID generato in modo casuale nella richiesta di autenticazione. Ad esempio, includi l’ID nel campo del nome utente.
1. L&#39;azione indicata nel passaggio 2 comporterà l&#39;invio di una richiesta di autenticazione da parte di Primetime DRM al server del cliente. La richiesta include il certificato del dispositivo:
   1. Il server estrae il certificato del dispositivo e l’ID generato dalla richiesta e memorizza.
   1. Il sottosistema del cliente pregenera le licenze per questo certificato del dispositivo, le memorizza e concede l’accesso ad esse in modo da associarle all’ID generato. .
1. Il server risponde alla richiesta con un messaggio di operazione riuscita.
1. L&#39;applicazione memorizza l&#39;ID generato.

Dopo la registrazione del dispositivo, l’applicazione utilizza l’ID generato nello stesso modo in cui avrebbe utilizzato l’ID dispositivo nello schema precedente:
1. L&#39;applicazione tenterà di individuare l&#39;ID generato.
1. Se l&#39;ID generato viene trovato, l&#39;applicazione utilizzerà l&#39;ID generato durante il download delle licenze pregenerate. L&#39;applicazione invierà le licenze al client DRM Primetime per l&#39;utilizzo utilizzando `DRMManager.storeVoucher()` metodo. .
1. Se l’ID generato non viene trovato, l’applicazione passerà attraverso la procedura di registrazione del dispositivo.

## Ripristino di fabbrica DRM {#drm-factory-reset}

Quando l&#39;utente del dispositivo richiama l&#39;opzione DRM factory reset, il certificato del dispositivo viene eliminato. Per continuare la riproduzione del contenuto protetto, l’applicazione deve seguire nuovamente la procedura di registrazione del dispositivo. Se l&#39;applicazione invia una licenza pregenerata obsoleta, il client DRM di Primetime la rifiuterà poiché la licenza è stata crittografata per un ID dispositivo precedente.

* API Flash: [DRMManager.resetDRMVouchers()](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/net/drm/DRMManager.html#resetDRMVouchers()) - (Può essere richiamato solo in risposta a determinati codici di errore DRM non recuperabili).
* API iOS: [DRMManager resetDRM](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a0dd6c9662428583196e0419d3ea69446)
* API Android: [DRMManager.resetDRM()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#resetDRM(com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMOperationCompleteCallback))
