---
seo-title: Panoramica delle licenze fuori banda
title: Panoramica delle licenze fuori banda
uuid: 82e4529a-ee1b-4c0c-8885-e0e68319d1a0
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 0%

---


# Licenze fuori banda {#out-of-band-licenses}

È inoltre possibile ottenere licenze fuori banda (senza contattare un server licenze Primetime DRM) memorizzando la licenza su disco e in memoria utilizzando il metodo `storeVoucher()`.

Per riprodurre video crittografati in Primetime, il runtime interessato deve ottenere la licenza per quel video. La licenza contiene la chiave di decrittazione del video ed è generata dal server licenze DRM Primetime che il cliente ha distribuito.

In genere, il runtime ottiene questa licenza inviando una richiesta di licenza al server licenze DRM Primetime indicato nei metadati DRM del video ( `DRMContentData` classe). L&#39;applicazione può attivare questa richiesta di licenza chiamando il metodo `DRMManager.loadVoucher()`.

`DRMManager.storeVoucher()` consente alla domanda di inviare licenze ottenute fuori banda. Il runtime può quindi saltare il processo di richiesta della licenza e utilizzare le licenze inoltrate per riprodurre video crittografati. La licenza deve ancora essere generata dal server licenze Primetime DRM prima che possa essere ottenuta fuori banda. Tuttavia, potete scegliere di ospitare le licenze su qualsiasi server HTTP, invece di un server licenze DRM Primetime.

`DRMManager.storeVoucher()` viene inoltre utilizzato per supportare la condivisione delle licenze tra più dispositivi. Dopo Primetime DRM 3.0, questa funzione è denominata &quot;Supporto del dominio del dispositivo&quot;. Se la distribuzione supporta questo caso di utilizzo, è possibile registrare più computer a un gruppo di dispositivi utilizzando il metodo `DRMManager.addToDeviceGroup()`. Se è presente un computer con una licenza valida associata a un dominio per un determinato contenuto, l&#39;applicazione può quindi estrarre la licenza serializzata utilizzando il metodo `DRMVoucher.toByteArray()` e sugli altri computer è possibile importare le licenze utilizzando il metodo `DRMManager.storeVoucher()`.

## Informazioni sulla registrazione del dispositivo {#about-device-registration}

Tutte le licenze DRM Primetime, al momento della creazione, devono essere associate a un&#39;entità finale. Il binding è il processo crittografico che consente a una specifica entità di utilizzare solo la licenza. Ciò è necessario per evitare &quot;licenze galleggianti&quot; che possono essere utilizzate da qualsiasi dispositivo arbitrario. Affinché le licenze DRM di Primetime siano &quot;pre-generate&quot;, significa che il &quot;target&quot; di queste licenze pregenerate deve essere noto in anticipo. Primetime DRM fa riferimento a questo come &quot;Device Registration&quot; (Registrazione dispositivo).

## Registrare un dispositivo {#register-a-device}

Supponiamo che siano state eseguite le seguenti attività:

* Hai impostato Primetime DRM Server SDK.
* È stato configurato un server HTTP per il rilascio di licenze pre-generate.
* È stata creata un&#39;applicazione Primetime per visualizzare il contenuto protetto.

 La fase di registrazione del dispositivo include le azioni seguenti:

1. L’applicazione crea un ID generato in modo casuale.
1. L&#39;applicazione richiama il metodo `DRMManager.authenticate()`. L&#39;applicazione deve includere l&#39;ID generato in modo casuale nella richiesta di autenticazione. Ad esempio, includete l’ID nel campo del nome utente.
1. L&#39;azione di cui al Passaggio 2 comporterà l&#39;invio da parte di DRM di Primetime di una richiesta di autenticazione al server del cliente. Questa richiesta include il certificato del dispositivo:
   1. Il server estrae il certificato del dispositivo e l’ID generato dalla richiesta e memorizza.
   1. Il sottosistema del cliente pre-genera le licenze per questo certificato dispositivo, le memorizza e concede l&#39;accesso a tali licenze in modo da associarle all&#39;ID generato. .
1. Il server risponde alla richiesta con un messaggio &quot;success&quot;.
1. L&#39;applicazione memorizza l&#39;ID generato.

Dopo la registrazione del dispositivo, l&#39;applicazione utilizza l&#39;ID generato nello stesso modo in cui avrebbe utilizzato l&#39;ID dispositivo nello schema precedente:
1. L&#39;applicazione tenterà di individuare l&#39;ID generato.
1. Se viene trovato l&#39;ID generato, l&#39;applicazione utilizzerà l&#39;ID generato durante il download delle licenze pre-generate. L&#39;applicazione invierà le licenze al client DRM Primetime per l&#39;utilizzo utilizzando il metodo `DRMManager.storeVoucher()`. .
1. Se l&#39;ID generato non viene trovato, l&#39;applicazione passerà attraverso la procedura di registrazione del dispositivo.

## Reimpostazione della fabbrica DRM {#drm-factory-reset}

Quando l&#39;utente del dispositivo richiama l&#39;opzione di ripristino della fabbrica DRM, il certificato del dispositivo viene eliminato. Per continuare la riproduzione del contenuto protetto, l&#39;applicazione deve seguire di nuovo la procedura di registrazione del dispositivo. Se l&#39;applicazione invia una licenza pre-generata obsoleta, il client DRM Primetime la rifiuterà poiché la licenza è stata crittografata per un ID dispositivo precedente.

* API Flash: [DRMManager.resetDRMVouchers()](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/net/drm/DRMManager.html#resetDRMVouchers()) - (È possibile chiamare solo in risposta ad alcuni codici di errore DRM non recuperabili).
* API iOS: [DRMManager resetDRM](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a0dd6c9662428583196e0419d3ea69446)
* API Android: [DRMManager.resetDRM()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#resetDRM(com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMOperationCompleteCallback))