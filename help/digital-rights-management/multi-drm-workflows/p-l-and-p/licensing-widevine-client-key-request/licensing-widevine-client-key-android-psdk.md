---
description: Il codice client trasmette i dati a un'API Android.
seo-description: Il codice client trasmette i dati a un'API Android.
seo-title: Flusso di lavoro della richiesta chiave in Android PSDK
title: Flusso di lavoro della richiesta chiave in Android PSDK
uuid: 575163de-0f96-434d-a3ff-7e114caf72de
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Flusso di lavoro della richiesta chiave in Android PSDK{#key-request-workflow-on-android-psdk}

Il codice client trasmette i dati a un&#39;API Android.

Su Android, il codice client deve trasmettere l’URL del server delle licenze e i dati di acquisizione delle licenze tramite le seguenti API:

```
class DRMManager 
   { 
   ... 
   /* 
   * Set the license server URL and attached request properties that the PSDK should use for the passed in drm type.  
   * 
   * drmType: "com.widevine.alpha" for widevine. "com.microsoft.playready" for playready. 
   * licenseServerURL: self explanatory.  
   * requestProperties: key value pairs to be attached as HTTP headers to all license request sent to the passed in license server URL. Pass in 
   * NULL if none is needed.  
   */ 
   public static void setProtectionData(String drmType, String licenseServerURL,  Map<String, String> requestProperties); 
    }
```

Dopo aver chiamato questa API, il codice può avviare la riproduzione del contenuto nel modo usuale. Se utilizzate Expressplay, potete trasmettere il token come parte dell’URL del server delle licenze o come proprietà di richiesta e rimuovere il token dall’URL del server delle licenze.

Alcuni dispositivi Android supportano sia Widevine che PlayReady. Su tali dispositivi il cliente potrebbe voler forzare PSDK a decifrare il contenuto utilizzando un DRM particolare se il contenuto ha più intestazioni DRM. Questa operazione può essere eseguita chiamando la seguente API prima della riproduzione:

```
class MediaPlayer 
   { 
   ... 
    
   /* 
   * drm: pass in "com.widevine.alpha" for widevine or "com.microsoft.playready" for playready 
   * 
   */ 
   public void setDRMScheme(String drm) throws MediaPlayerException 
   }
```

