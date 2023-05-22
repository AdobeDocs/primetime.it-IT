---
description: Puoi utilizzare il DRM widevine nativo per Android con i flussi DASH.
title: DRM widevine
exl-id: 6a011cd7-446a-4f3a-ae36-110618001bf3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '72'
ht-degree: 0%

---

# DRM widevine {#widevine-drm}

Puoi utilizzare il DRM widevine nativo per Android con i flussi DASH.

Chiama quanto segue `com.adobe.mediacore.drm.DRMManager` API prima di avviare la riproduzione:

```java
public static void setProtectionData( 
    String drm,  
    String licenseServerURL,   
    Map<String, String> requestProperties)
```

Argomenti:

* `drm` - `"com.widevine.alpha"` per Widevine.

* `licenseServerURL` : URL del server licenze Widevine che riceve le richieste di licenza.
* `requestProperties` - Contiene intestazioni aggiuntive da includere nella richiesta di licenza in uscita.

Ad esempio, quando si utilizza contenuto incluso nel pacchetto per Expressplay DRM, utilizzare il codice seguente prima della riproduzione:

```java
DRMManager.setProtectionData( 
  "com.widevine.alpha",  
  "https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken= 
<i>token</i>",  
  null); 
```
