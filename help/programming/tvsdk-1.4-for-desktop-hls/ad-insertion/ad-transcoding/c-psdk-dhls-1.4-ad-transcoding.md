---
description: Alcuni annunci di terze parti (o creativi) non possono essere uniti nel flusso di contenuto HTTP Live Streaming (HLS) perché il loro formato video è incompatibile con HLS. L’inserimento di annunci Primetime e TVSDK possono tentare facoltativamente di ricompattare gli annunci incompatibili in video M3U8 compatibili.
title: Ricomprimi annunci incompatibili utilizzando Adobe Creative Repackaging Service
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---


# Ricomprimi annunci incompatibili utilizzando Adobe Creative Repackaging Service {#repackage-incompatible-ads-using-adobe-creative-repackaging-service}

Alcuni annunci di terze parti (o creativi) non possono essere uniti nel flusso di contenuto HTTP Live Streaming (HLS) perché il loro formato video è incompatibile con HLS. L’inserimento di annunci Primetime e TVSDK possono tentare facoltativamente di ricompattare gli annunci incompatibili in video M3U8 compatibili.

Gli annunci forniti da varie terze parti, come un agenzia ad server, il tuo partner di inventario o una rete pubblicitaria, vengono spesso consegnati in formati incompatibili, come ad esempio il progressivo download MP4.

Quando TVSDK incontra per la prima volta un annuncio non compatibile, il lettore ignora l&#39;annuncio e invia una richiesta al servizio di ricompilazione creativa (CRS), che fa parte del back end di inserimento degli annunci Primetime, per ricompattare l&#39;annuncio in un formato compatibile. CRS tenta di generare rappresentazioni M3U8 a più bit-rate dell’annuncio e le memorizza sulla rete CDN (Content Delivery Network) di Primetime. La prossima volta che TVSDK riceve una risposta pubblicitaria che punta a quell&#39;annuncio, il lettore utilizza la versione M3U8 compatibile con HLS dalla CDN.

Per abilitare questa funzione opzionale, contatta il tuo rappresentante di Adobe.

Per ulteriori informazioni su CRS, consulta [Creative Packaging Service (CRS)](https://helpx.adobe.com/content/dam/help/en/primetime/guides/crs.pdf).

## Supporto di più CDN per CRS e consegna di annunci {#multiple-cdn-support-for-crs-ad-delivery}

Mentre lo scenario predefinito del servizio di ricompilazione creativa (CRS) è quello di utilizzare una rete di dati di contenuto (CDN), puoi distribuire le risorse CRS su più di una rete CDN.

Puoi utilizzare più CDN per i seguenti motivi:

* Un requisito per l&#39;ingrandimento di eventi di visualizzazione di grandi dimensioni.
* Un requisito per far corrispondere l’origine CDN della risorsa CRS con l’origine CDN del contenuto principale.

Puoi trasformare l’URL predefinito fornito dal CRS utilizzando le API di trasformazione URL TVSDK.

Di seguito sono elencate le aggiunte API in TVSDK:

* `URLTransformer` Interfaccia che descrive i metodi necessari per trasformare gli URL e i CRS richiesti da TVSDK. Le applicazioni possono implementare questa interfaccia e fornire implementazioni per i metodi richiesti.

* `DefaultURLTransformer` L’istanza di trasformazione URL predefinita creata in TVSDK e che implementa l’ `URLTransformer` interfaccia. Le applicazioni possono ignorare questa classe o aggiungere un gestore di trasformazione post URL. Questo gestore è utile quando l&#39;applicazione desidera apportare modifiche alla richiesta URL dopo che la trasformazione predefinita è stata applicata.

* `NetworkConfiguration.urlTransformer` Un metodo setter fornito sull&#39;istanza di  `NetworkConfiguration` metadati per impostare l&#39; `URLTransformer` implementazione.

>[!IMPORTANT]
>
>Le implementazioni dell&#39;app devono verificare la presenza dell&#39;enumerazione `URLTransformerInputType` e trasformare solo gli URL di tipo `URLTransformerInputType.CRSCreative` per CRS.

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
