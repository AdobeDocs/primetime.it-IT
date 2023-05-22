---
description: Alcuni annunci di terze parti (o creativi) non possono essere uniti nel flusso di contenuto HTTP Live Streaming (HLS) perché il loro formato video è incompatibile con HLS. Primetime ad insertion e TVSDK possono opzionalmente tentare di ricompilare gli annunci incompatibili in video M3U8 compatibili.
title: Riconfezionamento di annunci incompatibili con Adobe Creative Repackaging Service
exl-id: 8c3e5baf-1941-4330-a4b7-61ed623dfd5e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---

# Riconfezionamento di annunci incompatibili con Adobe Creative Repackaging Service {#repackage-incompatible-ads-using-adobe-creative-repackaging-service}

Alcuni annunci di terze parti (o creativi) non possono essere uniti nel flusso di contenuto HTTP Live Streaming (HLS) perché il loro formato video è incompatibile con HLS. Primetime ad insertion e TVSDK possono opzionalmente tentare di ricompilare gli annunci incompatibili in video M3U8 compatibili.

Gli annunci forniti da terze parti, come ad esempio un server di annunci di un&#39;agenzia, un partner di inventario o una rete di annunci, vengono spesso consegnati in formati incompatibili, come ad esempio MP4 con download progressivo.

Quando TVSDK rileva per la prima volta un annuncio incompatibile, il lettore ignora l’annuncio e invia una richiesta al servizio di repackaging creativo (CRS), che fa parte del back-end di inserimento dell’annuncio Primetime, per riconfezionare l’annuncio in un formato compatibile. CRS tenta di generare copie trasformate M3U8 a più bit rate dell’annuncio e memorizza tali copie trasformate sulla rete CDN (Content Delivery Network) Primetime. La prossima volta che TVSDK riceve una risposta dell’annuncio che punta a tale annuncio, il lettore utilizza la versione M3U8 compatibile con HLS dalla CDN.

Per abilitare questa funzione opzionale, contatta il rappresentante del tuo Adobe.

Per ulteriori informazioni su CRS, consulta [Creative Packaging Service (CRS)](https://helpx.adobe.com/content/dam/help/en/primetime/guides/crs.pdf).

## Supporto di più CDN per la distribuzione di annunci CRS{#multiple-cdn-support-for-crs-ad-delivery}

Anche se lo scenario predefinito del Servizio di reimballaggio creativo (CRS) prevede l’utilizzo di una rete CDN (Content Data Network), è possibile distribuire le risorse CRS su più di una rete CDN.

Puoi utilizzare più CDN per i seguenti motivi:

* È necessario aumentare la scalabilità per gli eventi di visualizzazione di grandi dimensioni.
* Requisito per la corrispondenza tra l’origine CDN della risorsa CRS e l’origine CDN del contenuto principale.

Puoi trasformare l’URL predefinito fornito da CRS utilizzando le API TVSDK URL Transformer.

Di seguito sono riportate le aggiunte API in TVSDK:

* `URLTransformer` Interfaccia che descrive i metodi necessari per trasformare gli URL degli annunci CRS richiesti da TVSDK. Le applicazioni possono implementare questa interfaccia e fornire implementazioni per i metodi richiesti.

* `DefaultURLTransformer` L’istanza di trasformazione URL predefinita creata in TVSDK e che implementa `URLTransformer` di rete. Le applicazioni possono ignorare questa classe o aggiungere un gestore di trasformazione post URL. Questo gestore è utile quando l’applicazione desidera apportare modifiche alla richiesta URL dopo l’applicazione della trasformazione predefinita.

* `NetworkConfiguration.setURLTransformer` Metodo di impostazione fornito sulla `NetworkConfiguration` istanza di metadati per impostare `URLTransformer` implementazione.

>[!IMPORTANT]
>
>Le implementazioni dell’app devono verificare la presenza di `URLTransformerInputType` enumerazione e solo URL di trasformazione di tipo `URLTransformerInputType.CRSCreative` per CRS.

Nell&#39;esempio di codice riportato di seguito viene illustrato come l&#39;applicazione può modificare il componente host predefinito in una stringa diversa, ad esempio `cdn.mycrsdomain.com`):

```java
NetworkConfiguration networkConfiguration = new NetworkConfiguration(); 
DefaultURLTransformer urlTransformer = new DefaultURLTransformer(); 
urlTransformer.addPostURLTransformHandler(new DefaultURLTransformer.URLTransformHandler() { 
    @Override 
    public String call(String url, URLTransformerInputType type) { 
        if (type == URLTransformerInputType.CRSCreative) { 
            try { 
                return url.replaceAll(new java.net.URI(url).getHost(), "cdn.mycrsdomain.com"); 
            } catch (URISyntaxException e) { 
            } 
        } 
        return url; 
    } 
}); 
   
networkConfiguration.setURLTransformer(urlTransformer); 
   
// metadata is the Metadata instance set on a MediaResource instance. 
metadata.setNode(DefaultMetadataKeys.NETWORK_CONFIGURATION.getValue(), networkConfiguration);
```
