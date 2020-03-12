---
description: Potete utilizzare le funzioni del sistema DRM (Digital Rights Management) di Primetime per fornire un accesso protetto ai contenuti video. In alternativa, puoi utilizzare soluzioni DRM di terze parti come alternativa alla soluzione integrata di Adobe.
seo-description: Potete utilizzare le funzioni del sistema DRM (Digital Rights Management) di Primetime per fornire un accesso protetto ai contenuti video. In alternativa, puoi utilizzare soluzioni DRM di terze parti come alternativa alla soluzione integrata di Adobe.
seo-title: DRM Widevine
title: DRM Widevine
uuid: 3a5fd786-4319-4e92-83b6-0f5328df6a44
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# DRM Widevine {#widevine-drm}

Potete utilizzare le funzioni del sistema DRM (Digital Rights Management) di Primetime per fornire un accesso protetto ai contenuti video. In alternativa, puoi utilizzare soluzioni DRM di terze parti come alternativa alla soluzione integrata di Adobe.

Per informazioni aggiornate sulla disponibilità di soluzioni DRM di terze parti, contattate il vostro rappresentante Adobe.

<!--<a id="section_1385440013EF4A9AA45B6AC98919E662"></a>-->

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
