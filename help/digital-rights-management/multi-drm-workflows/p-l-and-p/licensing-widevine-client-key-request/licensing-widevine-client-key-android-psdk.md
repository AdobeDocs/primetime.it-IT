---
description: Il codice client trasmette i dati a un’API Android.
title: Flusso di lavoro delle richieste chiave su PSDK Android
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---

# Flusso di lavoro delle richieste chiave su PSDK Android{#key-request-workflow-on-android-psdk}

Il codice client trasmette i dati a un’API Android.

Su Android, il codice client deve passare nell’URL del server licenze e nei dati di acquisizione della licenza corrispondenti utilizzando la seguente API:

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

Dopo aver chiamato correttamente questa API, il codice può quindi avviare la riproduzione del contenuto nel solito modo. Se si utilizza Expressplay, è possibile passare il token come parte dell&#39;URL del server licenze oppure come proprietà di richiesta e rimuovere il token dall&#39;URL del server licenze.

Alcuni dispositivi Android supportano sia Widevine che PlayReady. Su tali dispositivi il cliente potrebbe voler forzare PSDK a decrittografare il contenuto utilizzando un determinato DRM se il contenuto ha più intestazioni DRM. Questa operazione può essere eseguita chiamando la seguente API prima della riproduzione:

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
