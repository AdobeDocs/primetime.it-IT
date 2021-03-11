---
description: Il supporto per l'attributo withCredentials in XMLHttpRequests consente alle richieste di condivisione delle risorse tra origini (CORS) di includere i cookie del dominio di destinazione per diversi tipi di richieste.
keywords: CORS;origini incrociate;condivisione risorse;cookie;con credenziali
title: Condivisione delle risorse tra le origini
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---


# Condivisione delle risorse tra le origini {#cross-origin-resource-sharing}

Il supporto per l&#39;attributo withCredentials in XMLHttpRequests consente alle richieste di condivisione delle risorse tra origini (CORS) di includere i cookie del dominio di destinazione per diversi tipi di richieste.

Quando il client richiede un manifesto, un segmento o una chiave, il server può impostare un cookie che il client deve trasmettere per le richieste successive. Per consentire la lettura e la scrittura di cookie, il client deve impostare l’attributo `withCredentials` su `true` per le richieste di origini diverse.

Per abilitare il supporto `withCredentials` per la maggior parte dei tipi di richieste durante la riproduzione di una determinata risorsa multimediale:

1. Creare l&#39;oggetto `CORSConfig` .

   ```js
   var corsConfig = new AdobePSDK.CORSConfig();  
   corsConfig.enableEncryptionRequest = true; 
   ```

1. Allega l’ `corsConfig` all’oggetto `NetworkConfiguration` e imposta `useCookieHeaderForAllRequests` su `true`.

   ```js
   var networkConfig = new AdobePSDK.NetworkConfiguration();  
   networkConfig.CORSConfig = corsConfig; 
   networkConfiguration.useCookieHeaderForAllRequests= true;
   ```

1. Impostare `networkConfig` nell&#39;oggetto `MediaPlayerItemConfig`.

   ```js
   var mediaPlayerItemConfig = new AdobePSDK.MediaPlayerItemConfig();  
   mediaPlayerItemConfig.networkConfiguration = networkConfig; 
   ```

1. Passa `MediaPlayerItemConfig` al metodo `MediaPlayer.replaceCurrentResource` .

   ```js
   var player = new AdobePSDK.MediaPlayer(); 
   mediaResource = new AdobePSDK.MediaResource(url, AdobePSDK.MediaResourceType.HLS);  
   
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);  
   ```

>[!IMPORTANT]
>
>Il flag `useCookieHeaderForAllRequests` non influisce sulle richieste di licenza. Per impostare l&#39;attributo `withCredentials` su `true` per una richiesta di licenza, è necessario impostare l&#39;attributo `withCredentials` nei dati di protezione o specificare una chiave di autorizzazione nel `httpRequestHeaders` dei dati di protezione. Ad esempio:

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

Il flag non influisce su una richiesta di licenza perché alcuni server impostano il campo `Access-Control-Allow-Origin` sul carattere jolly (&#39;*&#39;) nella risposta. Tuttavia, quando il flag delle credenziali è impostato su `true`, il carattere jolly non può essere utilizzato in `Access-Control-Allow-Origin`. Se si imposta `useCookieHeaderForAllRequests` su `true` per tutti i tipi di richieste, è possibile che venga visualizzato il seguente errore per una richiesta di licenza:

Ricorda le seguenti informazioni:

* Quando una chiamata con `withCredentials=true` non riesce, il browser TVSDK prova nuovamente la chiamata senza `withCredentials`.
* Quando si effettua una chiamata con `networkConfiguration.useCookieHeaderForAllRequests=false`, le richieste XHR vengono effettuate senza l’attributo `withCredentials` .