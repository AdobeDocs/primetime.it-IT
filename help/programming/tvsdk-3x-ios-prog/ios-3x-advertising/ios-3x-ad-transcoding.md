---
description: Alcuni annunci di terze parti (o creativi) non possono essere uniti nel flusso di contenuto HTTP Live Streaming (HLS) perché il loro formato video è incompatibile con HLS. Primetime ad insertion e TVSDK possono opzionalmente tentare di ricompilare gli annunci incompatibili in video M3U8 compatibili.
title: Riconfezionamento di annunci incompatibili con Adobe Creative Repackaging Service
exl-id: 86a8bd94-4de0-4aba-b6ee-4e0e1ee864c8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---

# Riconfezionamento di annunci incompatibili con Adobe Creative Repackaging Service {#repackage-incompatible-ads-using-adobe-creative-repackaging-service}

Alcuni annunci di terze parti (o creativi) non possono essere uniti nel flusso di contenuto HTTP Live Streaming (HLS) perché il loro formato video è incompatibile con HLS. Primetime ad insertion e TVSDK possono opzionalmente tentare di ricompilare gli annunci incompatibili in video M3U8 compatibili.

Gli annunci forniti da terze parti, come ad esempio un server di annunci di un&#39;agenzia, un partner di inventario o una rete di annunci, vengono spesso consegnati in formati incompatibili, come ad esempio MP4 con download progressivo.

Quando TVSDK rileva per la prima volta un annuncio incompatibile, il lettore ignora l’annuncio e invia una richiesta al servizio di repackaging creativo (CRS), che fa parte del back-end di inserimento dell’annuncio Primetime, per riconfezionare l’annuncio in un formato compatibile. CRS tenta di generare copie trasformate M3U8 a più bit rate dell’annuncio e memorizza tali copie trasformate sulla rete CDN (Content Delivery Network) Primetime. La prossima volta che TVSDK riceve una risposta dell’annuncio che punta a tale annuncio, il lettore utilizza la versione M3U8 compatibile con HLS dalla CDN.

Per abilitare questa funzione opzionale, contatta il rappresentante del tuo Adobe.

## Supporto di più CDN per la distribuzione di annunci CRS {#section_900FDDA5454143718F1EB4C9732C8E1C}

Anche se lo scenario predefinito del Servizio di reimballaggio creativo (CRS) prevede l’utilizzo di una rete CDN (Content Data Network), è possibile distribuire le risorse CRS su più di una rete CDN.

Puoi utilizzare più CDN per i seguenti motivi:

* È necessario aumentare la scalabilità per gli eventi di visualizzazione di grandi dimensioni.
* Requisito per la corrispondenza tra l’origine CDN della risorsa CRS e l’origine CDN del contenuto principale.

Puoi trasformare l’URL predefinito fornito da CRS utilizzando le API TVSDK URL Transformer.

Di seguito sono riportate le aggiunte API in TVSDK:

* `PTURLTransformer` Protocollo che descrive i metodi necessari per trasformare gli URL degli annunci CRS richiesti da TVSDK. Le applicazioni possono implementare questo protocollo e fornire implementazioni per i metodi richiesti.

* `PTDefaultURLTransformer` L’istanza di trasformazione URL predefinita creata in TVSDK e che implementa `PTURLTransformer` protocollo. Le applicazioni possono ignorare questa classe o aggiungere un gestore di trasformazione post URL. Questo gestore è utile quando l’applicazione desidera apportare modifiche alla richiesta URL dopo l’applicazione della trasformazione predefinita.

* `PTNetworkConfiguration setURLTransformer:defaultTransformer` Metodo di impostazione fornito sulla `PTNetworkConfiguration` istanza di metadati per impostare `PTURLTransformer` implementazione.

>[!IMPORTANT]
>
>Le implementazioni dell’app devono verificare la presenza di `PTURLTransformerInputType` enumerazione e solo URL di trasformazione di tipo `PTURLTransformerInputTypeCRSCreative` per CRS.

Nell&#39;esempio di codice riportato di seguito viene illustrato come l&#39;applicazione può modificare il componente host predefinito in una stringa diversa, ad esempio `cdn.mycrsdomain.com`):

```
// The sample code below uses Non-ARC code 
PTNetworkConfiguration *networkConfiguration = [[[PTNetworkConfiguration alloc] init] autorelease]; 
   
PTDefaultURLTransformer *defaultTransformer = [[[PTDefaultURLTransformer alloc] init] autorelease]; 
    [defaultTransformer addPostURLTransformHandler:^NSString *(NSString *url, PTURLTransformerInputType type) { 
        if (type == PTURLTransformerInputTypeCRSCreative) { 
            return [url stringByReplacingOccurrencesOfString:[NSURL URLWithString:url].host  
              withString:@"cdn.mycrsdomain.com"]; 
        } 
            return url; 
    }]; 
  
[networkConfiguration setURLTransformer:defaultTransformer]; 
   
// metadata is the PTMetadata instance set on a PTMediaPlayerItem instance. 
[metadata setMetadata:[self getNetworkConfiguration] forKey:PTNetworkConfigurationMetadataKey];
```
