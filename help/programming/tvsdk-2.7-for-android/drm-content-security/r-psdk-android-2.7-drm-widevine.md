---
description: È possibile utilizzare il DRM Widevine nativo di Android con i flussi DASH.
seo-description: È possibile utilizzare il DRM Widevine nativo di Android con i flussi DASH.
seo-title: DRM Widevine
title: DRM Widevine
uuid: ceb2f18f-9e53-47d6-9d4b-7004ac1d22c9
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# DRM Widevine {#widevine-drm}

È possibile utilizzare il DRM Widevine nativo di Android con i flussi DASH.

Chiama la seguente `com.adobe.mediacore.drm.DRMManager` API prima di avviare la riproduzione:

```java
public static void setProtectionData( 
    String drm,  
    String licenseServerURL,   
    Map<String, String> requestProperties)
```

Argomenti:

* `drm` - `"com.widevine.alpha"` per Widevine.

* `licenseServerURL` - L&#39;URL del server licenze Widevine che riceve le richieste di licenza.
* `requestProperties` - Contiene intestazioni aggiuntive da includere nella richiesta di licenza in uscita.

Ad esempio, quando utilizzate contenuto incluso in un pacchetto per Express DRM, utilizzate il seguente codice prima di riprodurre:

```java
DRMManager.setProtectionData( 
  "com.widevine.alpha",  
  "https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken= 
<i>token</i>",  
  null); 
```

