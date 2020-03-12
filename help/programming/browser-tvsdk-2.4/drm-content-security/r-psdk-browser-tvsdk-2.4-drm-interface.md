---
description: Browser TVSDK fornisce un'interfaccia DRM che potete utilizzare per riprodurre contenuto protetto da diverse soluzioni DRM, tra cui FairPlay, PlayReady e Widevine.
seo-description: Browser TVSDK fornisce un'interfaccia DRM che potete utilizzare per riprodurre contenuto protetto da diverse soluzioni DRM, tra cui FairPlay, PlayReady e Widevine.
seo-title: Panoramica dell'interfaccia DRM
title: Panoramica dell'interfaccia DRM
uuid: b553ebad-8310-4517-8d97-ef8a1c5f4340
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Panoramica dell&#39;interfaccia DRM{#drm-interface-overview}

Browser TVSDK fornisce un&#39;interfaccia DRM che potete utilizzare per riprodurre contenuto protetto da diverse soluzioni DRM, tra cui FairPlay, PlayReady e Widevine.

<!--<a id="section_59994F2059B245E996E0776214804A0A"></a>-->

>[!IMPORTANT]
>
>Il supporto DRM è disponibile per i flussi MPEG-Dash protetti con i sistemi DRM Microsoft PlayReady (in Internet Explorer su Windows 8.1 e Edge) e Widevine (su Google Chrome). Il supporto DRM è disponibile per i flussi HLS su Safari protetti con FairPlay.

L&#39;interfaccia chiave del flusso di lavoro DRM è il `DRMManager`. È possibile ottenere un riferimento all’ `DRMManager` istanza tramite l’istanza MediaPlayer:

* `var mediaPlayer = new AdobePSDK.MediaPlayer();`
* `var drmManager = mediaPlayer.drmManager;`

<!--<a id="section_B7E8AD9A4D4F4BD9BA2A67ABC135D6F9"></a>-->

Di seguito è riportato un flusso di lavoro di alto livello per la riproduzione di contenuti protetti da DRM:

1. Per allegare i dati specifici del sistema DRM che saranno utilizzati da Browser TVSDK nel processo di acquisizione della licenza per un flusso protetto, effettua la seguente chiamata prima di richiamare `mediaPlayer.replaceCurrentResource`:

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

1. Se si prevede che lo stesso contenuto funzioni con diversi sistemi DRM in browser diversi, è possibile specificare i dati di protezione per più sistemi DRM.

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

1. Quando i dati di protezione non sono impostati, le informazioni necessarie, come l&#39;URL della licenza, vengono recuperate dalla casella PSSH per i sistemi DRM, se applicabile.

   >[!TIP]
   >
   >Se si specificano dati di protezione, l&#39;URL della licenza specificato nella casella PSSH viene sostituito.

1. Per impostazione predefinita, il tipo di sessione per la licenza DRM è temporaneo, il che significa che la licenza non viene memorizzata dopo la chiusura della sessione.

   Potete specificare un tipo di sessione utilizzando un&#39;API in `DRMManager`.  Per compatibilità con versioni precedenti, i tipi di sessione includono `temporary`, `persistent-license`, `persistent-usage-record`e `persistent`.

   ```js
   var drmManager = mediaPlayer.drmManager; 
    drmManager.setEMESessionType(“<YOUR_SESSION_TYPE>”); 
   ```

1. Quando l&#39; `sessionType` utilizzato è `persistent-license` o `persistent`, la licenza DRM può essere restituita richiamando `DRMManager.returnLicense`.

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

