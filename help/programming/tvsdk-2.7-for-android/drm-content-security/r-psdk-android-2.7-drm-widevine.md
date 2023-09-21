---
description: Puoi utilizzare il DRM widevine nativo per Android con i flussi DASH.
title: DRM widevine
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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
