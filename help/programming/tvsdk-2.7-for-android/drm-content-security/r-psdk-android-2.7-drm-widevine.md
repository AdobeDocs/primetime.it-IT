---
description: È possibile utilizzare il DRM nativo Widevine Android con flussi DASH.
title: DRM
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '72'
ht-degree: 0%

---


# DRM Widevine {#widevine-drm}

È possibile utilizzare il DRM nativo Widevine Android con flussi DASH.

Chiama la seguente `com.adobe.mediacore.drm.DRMManager` API prima di avviare la riproduzione:

```java
public static void setProtectionData( 
    String drm,  
    String licenseServerURL,   
    Map<String, String> requestProperties)
```

Argomenti:

* `drm` -  `"com.widevine.alpha"` per Widevine.

* `licenseServerURL` - L&#39;URL del server licenze Widevine che riceve richieste di licenza.
* `requestProperties` - Contiene intestazioni aggiuntive da includere nella richiesta di licenza in uscita.

Ad esempio, quando utilizzi il contenuto incluso nel pacchetto per Expressplay DRM, utilizza il codice seguente prima di riprodurre:

```java
DRMManager.setProtectionData( 
  "com.widevine.alpha",  
  "https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken= 
<i>token</i>",  
  null); 
```

