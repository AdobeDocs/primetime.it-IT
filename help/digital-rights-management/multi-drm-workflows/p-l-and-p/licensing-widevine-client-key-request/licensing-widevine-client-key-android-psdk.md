---
description: Il codice client trasmette i dati a un’API Android.
title: Flusso di lavoro della richiesta chiave in PSDK per Android
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---


# Flusso di lavoro della richiesta chiave su Android PSDK{#key-request-workflow-on-android-psdk}

Il codice client trasmette i dati a un’API Android.

Su Android, il codice client deve trasmettere l&#39;URL del server di licenza e i dati di acquisizione della licenza utilizzando la seguente API:

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

Dopo aver chiamato correttamente questa API, il codice può quindi avviare la riproduzione del contenuto nel modo consueto. Se utilizzi Expressplay, puoi passare il token come parte dell’URL del server licenze o come proprietà di richiesta e rimuovere il token dall’URL del server licenze.

Alcuni dispositivi Android supportano sia Widevine che PlayReady. Su tali dispositivi il cliente può voler forzare PSDK a decrittografare il contenuto utilizzando una particolare DRM se il contenuto ha più intestazioni DRM. Questa operazione può essere eseguita richiamando la seguente API prima della riproduzione:

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

