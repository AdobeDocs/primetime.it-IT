---
description: Il browser TVSDK fornisce un'interfaccia DRM da utilizzare per riprodurre contenuti protetti da diverse soluzioni DRM, tra cui FairPlay, PlayReady e Widevine.
title: Panoramica dell'interfaccia DRM
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---


# Panoramica dell&#39;interfaccia DRM{#drm-interface-overview}

Il browser TVSDK fornisce un&#39;interfaccia DRM da utilizzare per riprodurre contenuti protetti da diverse soluzioni DRM, tra cui FairPlay, PlayReady e Widevine.

<!--<a id="section_59994F2059B245E996E0776214804A0A"></a>-->

>[!IMPORTANT]
>
>Il supporto DRM è disponibile per i flussi MPEG-Dash protetti con i sistemi DRM Microsoft PlayReady (su Internet Explorer su Windows 8.1 e Edge) e Widevine (su Google Chrome). Il supporto DRM è disponibile per i flussi HLS su Safari protetti con FairPlay.

L’interfaccia chiave del flusso di lavoro DRM è `DRMManager`. Un riferimento all&#39;istanza `DRMManager` può essere ottenuto tramite l&#39;istanza MediaPlayer:

* `var mediaPlayer = new AdobePSDK.MediaPlayer();`
* `var drmManager = mediaPlayer.drmManager;`

<!--<a id="section_B7E8AD9A4D4F4BD9BA2A67ABC135D6F9"></a>-->

Ecco un flusso di lavoro di alto livello per la riproduzione di contenuti protetti da DRM:

1. Per allegare i dati specifici del sistema DRM che verranno utilizzati dal browser TVSDK nel processo di acquisizione della licenza per un flusso protetto, effettua la seguente chiamata prima di richiamare `mediaPlayer.replaceCurrentResource`:

   ```js
   var protectionData = { 
       "com.adobe.primetime": { 
          "serverURL": { 
             "individualization-request": "https://individualization.adobe.com/flashaccess/i15n/v5", 
             "license-request": "https://example.com:8096/flashaccess/req", 
             "license-release": "https://example.com:8096/flashaccess/req" 
          }, 
          "httpRequestHeaders": { 
          } 
       } 
   }; 
   var drmManager = mediaPlayer.drmManager; 
   drmManager.setProtectionData(protectionData);
   ```

1. Se lo stesso contenuto deve funzionare con sistemi DRM diversi in browser diversi, è possibile specificare i dati di protezione per più sistemi DRM.

   ```js
   var protectionData = { 
       "com.adobe.primetime": { 
           "serverURL": { 
               "individualization-request": "https://individualization.adobe.com/flashaccess/i15n/v5", 
               "license-request": "https://example.com:8096/flashaccess/req", 
               "license-release": "https://example.com:8096/flashaccess/req" 
           }, 
           "httpRequestHeaders": { 
           } 
       }, 
       "com.widevine.alpha": { 
           "serverURL": "https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken=<token value>", 
           "httpRequestHeaders": { 
               "dt-custom-data": "eyJ1c2VySWQiOiIxMjM0NS" 
           } 
       }, 
       "com.microsoft.playready": { 
           "serverURL": "https://pr.test.expressplay.com/playready/RightsManager.asmx?ExpressPlayToken=<token value>", 
           "httpRequestHeaders": { 
               "http-header-CustomData": "eyJ1c2VySWQiOiIxMjM0NS" 
           } 
       }, 
       "com.apple.fps.1_0": { 
           "serverURL": "https://fp.service.expressplay.com:80/hms/fp/rights/?ExpressPlayToken=<token value>", 
           "certificateURL": "Path_To_certificate.cer", 
           "licenseResponseType": "arraybuffer", 
           "httpRequestHeaders": { 
               "Content-type": "application/octet-stream" 
           } 
       }, 
       "org.w3.clearkey": { 
           "clearkeys": { 
               "H3JbV93QV3mPNBKQON2UtQ": "ClKhDPHMtCouEx1vLGsJsA", 
               "IAAAACAAIAAgACAAAAAAAg": "5t1CjnbMFURBou087OSj2w" 
           } 
       } 
   }; 
   
   var drmManager = mediaPlayer.drmManager; 
   drmManager.setProtectionData(protectionData);
   ```

1. Quando i dati di protezione non sono impostati, le informazioni necessarie, come l’URL della licenza, vengono recuperate dalla casella PSSH per i sistemi DRM, se applicabile.

   >[!TIP]
   >
   >La specificazione dei dati di protezione sostituisce l’URL della licenza specificato nella casella PSSH.

1. Per impostazione predefinita, il tipo di sessione per la licenza DRM è temporaneo, il che significa che la licenza non viene memorizzata dopo la chiusura della sessione.

   Puoi specificare un tipo di sessione utilizzando un&#39;API in `DRMManager`.  Per la compatibilità con le versioni precedenti, i tipi di sessione includono `temporary`, `persistent-license`, `persistent-usage-record` e `persistent`.

   ```js
   var drmManager = mediaPlayer.drmManager; 
    drmManager.setEMESessionType(“<YOUR_SESSION_TYPE>”); 
   ```

1. Quando il `sessionType` utilizzato è `persistent-license` o `persistent`, la licenza DRM può essere restituita richiamando `DRMManager.returnLicense`.

   ```js
   var onLicenseReturnFunc = function () { 
       console.log("DRM: License Return Complete "); 
   }, 
   
   onLicenseReturnErrorFunc = function (major, minor, errorString/*, errorServerUrl*/) { 
      console.log("DRM: License Return Error: " + errorString); 
   }, 
   
   drmManager = mediaPlayer.drmManager; 
   
   if (drmManager) { 
       var returnLicenseListener = new  
           AdobePSDK.DRMReturnLicenseListener(onLicenseReturnFunc, onLicenseReturnErrorFunc); 
       drmManager.returnLicense(null, null, null, false, returnLicenseListener, drmLicense.session); 
   }
   ```

