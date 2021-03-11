---
title: Distribuzione di contenuti
description: Distribuzione di contenuti
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 0%

---


# Distribuzione di contenuto {#delivering-content}

Primetime DRM è agnostico del meccanismo di consegna del contenuto mentre il runtime estrae il livello di rete e fornisce semplicemente il contenuto protetto al sottosistema DRM di Primetime. Pertanto, il contenuto può essere distribuito tramite HTTP, HTTP Dynamic Streaming, RTMP o RTMPE, HLS, ecc.

Tuttavia, a seconda del protocollo, potrebbero esserci intricazioni nel recupero dei metadati del contenuto protetto ( `DRMContentData` - di solito sotto forma di un file [!DNL .metadata] caricato su lato). Questi metadati DRM sono necessari per chiamare qualsiasi API `DRMManager`, ad esempio per prerecuperare la licenza, l’autenticazione DRM o per unirsi a un dominio del dispositivo. Ad esempio, con il protocollo RTMP/RTMPE, solo i dati FLV e F4V possono essere consegnati al cliente tramite il Flash Media Server (FMS). Per questo motivo, il client deve recuperare il BLOB di metadati in altri modi. Un&#39;opzione per risolvere questo problema è quella di ospitare i metadati su un server web HTTP e implementare il lettore video client per recuperare i metadati appropriati, a seconda del contenuto riprodotto.

```
private function getMetadata():void { 
    extrapolated-path-to-metadata = "https://metadatas.mywebserver.com/" + videoname; 
     var urlRequest : URLRequest =  
      new URLRequest(extrapolated-path-to-the-metadata + ".metadata");  
    var urlStream : URLStream = new URLStream();  
    urlStream.addEventListener(Event.COMPLETE, handleMetadata);  
    urlStream.addEventListener(IOErrorEvent.NETWORK_ERROR, handleIOError);  
    urlStream.addEventListener(IOErrorEvent.IO_ERROR, handleIOError);  
    urlStream.addEventListener(IOErrorEvent.VERIFY_ERROR, handleIOError);  
 
    try { 
        urlStream.load(urlRequest);  
    } catch(se:SecurityError) { 
        videoLog.text += se.toString() + "\n";  
    } catch(e:Error) { 
        videoLog.text += e.toString() + "\n";  
    } 
} 
```

