---
description: Il supporto per l'attributo withCredentials in XMLHttpRequests consente alle richieste di condivisione delle risorse tra origini (CORS) di includere i cookie del dominio di destinazione per diversi tipi di richieste.
keywords: CORS;cross origin;resource sharing;cookies;withCredentials
seo-description: Il supporto per l'attributo withCredentials in XMLHttpRequests consente alle richieste di condivisione delle risorse tra origini (CORS) di includere i cookie del dominio di destinazione per diversi tipi di richieste.
seo-title: Condivisione delle risorse tra le origini
title: Condivisione delle risorse tra le origini
uuid: e788b542-d4ac-48aa-91e2-1e88068cbba1
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Condivisione delle risorse tra le origini {#cross-origin-resource-sharing}

Il supporto per l&#39;attributo withCredentials in XMLHttpRequests consente alle richieste di condivisione delle risorse tra origini (CORS) di includere i cookie del dominio di destinazione per diversi tipi di richieste.

Quando il client richiede un manifesto, un segmento o una chiave, il server può impostare un cookie che il client deve trasmettere per le richieste successive. Per consentire la lettura e la scrittura di cookie, il client deve impostare l&#39; `withCredentials` attributo su `true` per le richieste tra origini diverse.

Per abilitare `withCredentials` il supporto per la maggior parte dei tipi di richieste durante la riproduzione di una determinata risorsa multimediale:

1. Creare l&#39; `CORSConfig` oggetto.

   ```js
   var corsConfig = new AdobePSDK.CORSConfig();  
   corsConfig.enableEncryptionRequest = true; 
   ```

1. Collegare l&#39;oggetto `corsConfig` all&#39; `NetworkConfiguration` oggetto e impostare `useCookieHeaderForAllRequests` su `true`.

   ```js
   var networkConfig = new AdobePSDK.NetworkConfiguration();  
   networkConfig.CORSConfig = corsConfig; 
   networkConfiguration.useCookieHeaderForAllRequests= true;
   ```

1. Impostato `networkConfig` nell&#39; `MediaPlayerItemConfig` oggetto.

   ```js
   var mediaPlayerItemConfig = new AdobePSDK.MediaPlayerItemConfig();  
   mediaPlayerItemConfig.networkConfiguration = networkConfig; 
   ```

1. Passa `MediaPlayerItemConfig` al `MediaPlayer.replaceCurrentResource` metodo.

   ```js
   var player = new AdobePSDK.MediaPlayer(); 
   mediaResource = new AdobePSDK.MediaResource(url, AdobePSDK.MediaResourceType.HLS);  
   
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);  
   ```

>[!IMPORTANT]
>
>Il `useCookieHeaderForAllRequests` flag non influenza le richieste di licenza. Per impostare l&#39; `withCredentials` attributo su `true` per una richiesta di licenza, è necessario impostare l&#39; `withCredentials` attributo nei dati di protezione o specificare una chiave di autorizzazione nei `httpRequestHeaders` dati di protezione. Ad esempio:

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

Il flag non influenza una richiesta di licenza perché alcuni server impostano il `Access-Control-Allow-Origin` campo su carattere jolly (&#39;*&#39;) nella risposta. Tuttavia, quando il flag delle credenziali è impostato su `true`, il carattere jolly non può essere utilizzato in `Access-Control-Allow-Origin`. Se impostate `useCookieHeaderForAllRequests` su `true` per tutti i tipi di richieste, per una richiesta di licenza potrebbe verificarsi il seguente errore:

Ricorda le informazioni seguenti:

* Quando una chiamata con `withCredentials=true` esito negativo, Browser TVSDK tenta di eseguire nuovamente la chiamata senza `withCredentials`.
* Quando si effettua una chiamata con `networkConfiguration.useCookieHeaderForAllRequests=false`, le richieste XHR vengono effettuate senza l’ `withCredentials` attributo.