---
seo-title: Distribuzione dei contenuti
title: Distribuzione dei contenuti
uuid: b277d369-fee3-4a20-9dd8-27b3a8a82a9e
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 0%

---


# Distribuzione di contenuto {#delivering-content}

Primetime DRM è agnostico al meccanismo di distribuzione del contenuto, in quanto il runtime estrae il livello di rete e fornisce semplicemente il contenuto protetto al sottosistema DRM di Primetime. Pertanto, il contenuto può essere distribuito tramite HTTP, HTTP Dynamic Streaming, RTMP o RTMPE, HLS, ecc.

Tuttavia, a seconda del protocollo, potrebbero essere presenti delle intricazioni nel recupero dei metadati del contenuto protetto ( `DRMContentData` - in genere sotto forma di un file [!DNL .metadata] caricato collateralmente). Questi metadati DRM sono necessari per chiamare qualsiasi API `DRMManager`, ad esempio per preacquisire la licenza, l&#39;autenticazione DRM o per unirsi a un dominio dispositivo. Ad esempio, con il protocollo RTMP/RTMPE, solo i dati FLV e F4V possono essere inviati al client tramite il Flash Media Server (FMS). Per questo motivo, il client deve recuperare il BLOB di metadati in altri modi. Un&#39;opzione per risolvere questo problema consiste nell&#39;ospitare i metadati su un server Web HTTP e implementare il lettore video client per recuperare i metadati appropriati, a seconda del contenuto riprodotto.

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

