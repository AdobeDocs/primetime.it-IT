---
description: Alcuni annunci (o creativi) di terze parti non possono essere inseriti nello streaming di contenuto HTTP Live Streaming (HLS) perché il loro formato video è incompatibile con HLS. L'inserimento di annunci Primetime e TVSDK possono eventualmente tentare di ricompilare annunci incompatibili in video M3U8 compatibili.
seo-description: Alcuni annunci (o creativi) di terze parti non possono essere inseriti nello streaming di contenuto HTTP Live Streaming (HLS) perché il loro formato video è incompatibile con HLS. L'inserimento di annunci Primetime e TVSDK possono eventualmente tentare di ricompilare annunci incompatibili in video M3U8 compatibili.
seo-title: Reimballaggio di annunci incompatibili con  Adobe Creative Repackaging Service
title: Reimballaggio di annunci incompatibili con  Adobe Creative Repackaging Service
uuid: 3bc24185-6b19-4660-bf78-5ccdaf14787a
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 0%

---


# Repacchetti di annunci incompatibili con  Adobe Creative Repackaging Service {#repackage-incompatible-ads-using-adobe-creative-repackaging-service}

Alcuni annunci (o creativi) di terze parti non possono essere inseriti nello streaming di contenuto HTTP Live Streaming (HLS) perché il loro formato video è incompatibile con HLS. L&#39;inserimento di annunci Primetime e TVSDK possono eventualmente tentare di ricompilare annunci incompatibili in video M3U8 compatibili.

Gli annunci inviati da varie terze parti, come un&#39;agenzia pubblicitaria server, il partner di magazzino o una rete di annunci, vengono spesso consegnati in formati incompatibili, come ad esempio il file MP4 per lo scaricamento progressivo.

Quando TVSDK incontra per la prima volta un annuncio incompatibile, il lettore ignora l&#39;annuncio e invia una richiesta al servizio di reimballaggio creativo (CRS), che fa parte del back end di inserimento annunci Primetime, per reassemblare l&#39;annuncio in un formato compatibile. CRS tenta di generare rappresentazioni M3U8 a bit rate multiplo dell’annuncio e memorizza tali rappresentazioni nella rete CDN (Primetime Content Delivery Network). Alla successiva ricezione di una risposta di annuncio da parte di TVSDK, il lettore utilizza la versione M3U8 compatibile con HLS dalla CDN.

Per abilitare questa funzione opzionale, contattate il rappresentante del Adobe .

Per ulteriori informazioni sui CRS, vedere [Creative Packaging Service (CRS)](https://helpx.adobe.com/content/dam/help/en/primetime/guides/crs.pdf).

## Supporto CDN multiplo per la distribuzione di annunci CRS {#multiple-cdn-support-for-crs-ad-delivery}

Mentre lo scenario predefinito di Creative Repackaging Service (CRS) prevede l’utilizzo di una rete CDN (Content Data Network), potete distribuire le risorse CRS su più CDN.

Potete usare più CDN per i seguenti motivi:

* Un requisito per la scalabilità per eventi di visualizzazione di grandi dimensioni.
* Requisito per far corrispondere l’origine CDN della risorsa CRS all’origine CDN del contenuto principale.

Potete trasformare l’URL predefinito fornito dal CRS utilizzando le API di trasformazione URL TVSDK.

Di seguito sono riportate le aggiunte API in TVSDK:

* `URLTransformer` Interfaccia che descrive i metodi necessari per trasformare gli URL e gli URL degli annunci CRS richiesti da TVSDK. Le applicazioni possono implementare questa interfaccia e fornire implementazioni per i metodi richiesti.

* `DefaultURLTransformer` L’istanza di trasformazione URL predefinita creata in TVSDK e che implementa l’ `URLTransformer` interfaccia. Le applicazioni possono ignorare questa classe o aggiungere un gestore di trasformazione post URL. Questo handler è utile quando l’applicazione desidera apportare modifiche alla richiesta URL dopo che è stata applicata la trasformazione predefinita.

* `NetworkConfiguration.urlTransformer` Metodo setter fornito sull’istanza di  `NetworkConfiguration` metadati per impostare l’ `URLTransformer` implementazione.

>[!IMPORTANT]
>
>Le implementazioni delle app devono verificare la presenza dell&#39;enumerazione `URLTransformerInputType` e trasformare solo gli URL di tipo `URLTransformerInputType.CRSCreative` per CRS.

L&#39;esempio di codice seguente mostra come l&#39;applicazione può modificare il componente host predefinito in una stringa diversa (ad esempio, `cdn.mycrsdomain.com`):

```
var networkConfiguration:NetworkConfiguration = new NetworkConfiguration(); 
   
var urlTransformer:DefaultURLTransformer = new DefaultURLTransformer(); 
urlTransformer.addPostURLTransformHandler(function (url:String, type:String) { 
    if (type == URLTransformerInputType.CRSCreative) { 
        return url.replace(URLUtil.getServerName(url), "cdn.mycrsdomain.com"); 
    } 
    return url; 
}); 
  
networkConfiguration.urlTransformer = urlTransformer; 
   
// metadata is the Metadata instance set on a MediaResource instance. 
metadata.setMetadata(DefaultMetadataKeys.NETWORK_CONFIGURATION_KEY,  
                     networkConfiguration);
```
