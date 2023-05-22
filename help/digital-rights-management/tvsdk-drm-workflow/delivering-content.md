---
title: Consegna dei contenuti
description: Consegna dei contenuti
copied-description: true
exl-id: a55293f0-ef9b-468f-a1b2-8222ebab0b4b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 0%

---

# Consegna dei contenuti {#delivering-content}

Primetime DRM è indipendente dal meccanismo di distribuzione dei contenuti, in quanto il runtime estrae il livello di rete e fornisce semplicemente i contenuti protetti al sottosistema DRM di Primetime. Pertanto, il contenuto può essere distribuito tramite HTTP, HTTP Dynamic Streaming, RTMP o RTMPE, HLS e così via.

Tuttavia, a seconda del protocollo, possono essere necessarie complessità per recuperare i metadati del contenuto protetto ( `DRMContentData` - generalmente sotto forma di caricatore laterale [!DNL .metadata] file). Questi metadati DRM sono necessari per chiamare qualsiasi `DRMManager` API, come preacquisizione della licenza, autenticazione DRM o aggiunta a un dominio del dispositivo. Ad esempio, con il protocollo RTMP/RTMPE, è possibile inviare al client solo i dati FLV e F4V tramite il Flash Media Server (FMS). Per questo motivo, il client deve recuperare il BLOB di metadati in altri modi. Un&#39;opzione per risolvere questo problema è ospitare i metadati su un server web HTTP e implementare il lettore video client per recuperare i metadati appropriati, a seconda del contenuto riprodotto.

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
