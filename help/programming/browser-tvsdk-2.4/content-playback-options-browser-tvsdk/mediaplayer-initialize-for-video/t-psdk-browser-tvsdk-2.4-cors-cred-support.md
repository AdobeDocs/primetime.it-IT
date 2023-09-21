---
description: Il supporto per l’attributo withCredentials in XMLHttpRequests consente alle richieste di condivisione delle risorse tra origini (CORS) di includere i cookie del dominio di destinazione per diversi tipi di richieste.
keywords: CORS;origine incrociata;condivisione risorse;cookie;conCredenziali
title: Condivisione delle risorse tra le origini
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# Condivisione delle risorse tra le origini {#cross-origin-resource-sharing}

Il supporto per l’attributo withCredentials in XMLHttpRequests consente alle richieste di condivisione delle risorse tra origini (CORS) di includere i cookie del dominio di destinazione per diversi tipi di richieste.

Quando il client richiede un manifesto, un segmento o una chiave, il server può impostare un cookie che il client deve trasmettere per le richieste successive. Per consentire la lettura e la scrittura di cookie, il client deve impostare `withCredentials` attribuire a `true` per le richieste tra origini diverse.

Per abilitare `withCredentials` supporto per la maggior parte dei tipi di richieste durante la riproduzione di una determinata risorsa multimediale:

1. Creare `CORSConfig` oggetto.

   ```js
   var corsConfig = new AdobePSDK.CORSConfig();  
   corsConfig.enableEncryptionRequest = true; 
   ```

1. Allega il `corsConfig` al `NetworkConfiguration` oggetto e set `useCookieHeaderForAllRequests` a `true`.

   ```js
   var networkConfig = new AdobePSDK.NetworkConfiguration();  
   networkConfig.CORSConfig = corsConfig; 
   networkConfiguration.useCookieHeaderForAllRequests= true;
   ```

1. Imposta `networkConfig` nel `MediaPlayerItemConfig` oggetto.

   ```js
   var mediaPlayerItemConfig = new AdobePSDK.MediaPlayerItemConfig();  
   mediaPlayerItemConfig.networkConfiguration = networkConfig; 
   ```

1. Superato `MediaPlayerItemConfig` al `MediaPlayer.replaceCurrentResource` metodo.

   ```js
   var player = new AdobePSDK.MediaPlayer(); 
   mediaResource = new AdobePSDK.MediaResource(url, AdobePSDK.MediaResourceType.HLS);  
   
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);  
   ```

>[!IMPORTANT]
>
>Il `useCookieHeaderForAllRequests` Questo flag non influisce sulle richieste di licenza. Per impostare `withCredentials` attribuire a `true` per una richiesta di licenza, è necessario impostare `withCredentials` nei dati di protezione o specificare una chiave di autorizzazione in `httpRequestHeaders` dei dati di protezione. Ad esempio:

```
# Example 1 
{ 
    "com.widevine.alpha": {  
        "withCredentials":true,  
        "serverURL":  
          "https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken=[YOUR_TOKEN</i]" } 
} 
 
# Example 2 
{ 
    "com.widevine.alpha": { 
        "httpRequestHeaders": {  
            "authorization": "true"  
            }, 
        "serverURL":  
          "https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken=[YOUR_TOKEN</i>]" }
        } 
}
```

Il flag non influisce su una richiesta di licenza perché alcuni server impostano `Access-Control-Allow-Origin` campo a carattere jolly (&#39;&#42;&#39;) nella loro risposta. Ma, quando il flag di credenziali è impostato su `true`, il carattere jolly non può essere utilizzato in `Access-Control-Allow-Origin`. Se si imposta `useCookieHeaderForAllRequests` a `true` per tutti i tipi di richieste, è possibile che venga visualizzato il seguente errore per una richiesta di licenza:

Tenere presenti le seguenti informazioni:

* Quando una chiamata con `withCredentials=true` non riesce, il browser TVSDK ritenta la chiamata senza `withCredentials`.
* Quando viene effettuata una chiamata con `networkConfiguration.useCookieHeaderForAllRequests=false`, le richieste XHR vengono effettuate senza `withCredentials` attributo.
