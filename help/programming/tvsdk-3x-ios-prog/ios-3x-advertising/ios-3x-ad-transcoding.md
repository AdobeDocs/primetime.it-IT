---
description: Alcuni annunci (o creativi) di terze parti non possono essere inseriti nello streaming di contenuto HTTP Live Streaming (HLS) perché il loro formato video è incompatibile con HLS. L'inserimento di annunci Primetime e TVSDK possono eventualmente tentare di ricompilare annunci incompatibili in video M3U8 compatibili.
seo-description: Alcuni annunci (o creativi) di terze parti non possono essere inseriti nello streaming di contenuto HTTP Live Streaming (HLS) perché il loro formato video è incompatibile con HLS. L'inserimento di annunci Primetime e TVSDK possono eventualmente tentare di ricompilare annunci incompatibili in video M3U8 compatibili.
seo-title: Reimballaggio di annunci incompatibili con Adobe Creative Repackaging Service
title: Reimballaggio di annunci incompatibili con Adobe Creative Repackaging Service
uuid: 56a2405d-b395-4fea-820d-343590be7c19
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# Reimballaggio di annunci incompatibili con Adobe Creative Repackaging Service {#repackage-incompatible-ads-using-adobe-creative-repackaging-service}

Alcuni annunci (o creativi) di terze parti non possono essere inseriti nello streaming di contenuto HTTP Live Streaming (HLS) perché il loro formato video è incompatibile con HLS. L&#39;inserimento di annunci Primetime e TVSDK possono eventualmente tentare di ricompilare annunci incompatibili in video M3U8 compatibili.

Gli annunci inviati da varie terze parti, come un&#39;agenzia pubblicitaria server, il partner di magazzino o una rete di annunci, vengono spesso consegnati in formati incompatibili, come ad esempio il file MP4 per lo scaricamento progressivo.

Quando TVSDK incontra per la prima volta un annuncio incompatibile, il lettore ignora l&#39;annuncio e invia una richiesta al servizio di reimballaggio creativo (CRS), che fa parte del back end di inserimento annunci Primetime, per reassemblare l&#39;annuncio in un formato compatibile. CRS tenta di generare rappresentazioni M3U8 a bit rate multiplo dell’annuncio e memorizza tali rappresentazioni nella rete CDN (Primetime Content Delivery Network). Alla successiva ricezione di una risposta di annuncio da parte di TVSDK, il lettore utilizza la versione M3U8 compatibile con HLS dalla CDN.

Per abilitare questa funzione opzionale, contattate il rappresentante Adobe.

Per ulteriori informazioni su CRS, consultate [Creative Packaging Service (CRS)](../../../dynamic-ad-insertion/creative-repackaging-service/crs-overview.md).

## Supporto CDN multiplo per la distribuzione di annunci CRS {#section_900FDDA5454143718F1EB4C9732C8E1C}

Mentre lo scenario predefinito di Creative Repackaging Service (CRS) prevede l’utilizzo di una rete CDN (Content Data Network), potete distribuire le risorse CRS su più CDN.

Potete usare più CDN per i seguenti motivi:

* Un requisito per la scalabilità per eventi di visualizzazione di grandi dimensioni.
* Requisito per far corrispondere l’origine CDN della risorsa CRS all’origine CDN del contenuto principale.

Potete trasformare l’URL predefinito fornito dal CRS utilizzando le API di trasformazione URL TVSDK.

Di seguito sono riportate le aggiunte API in TVSDK:

* `PTURLTransformer` Un protocollo che descrive i metodi necessari per trasformare gli URL e i CRS richiesti da TVSDK. Le applicazioni possono implementare questo protocollo e fornire implementazioni per i metodi richiesti.

* `PTDefaultURLTransformer` L’istanza di trasformazione URL predefinita creata in TVSDK e che implementa il `PTURLTransformer` protocollo. Le applicazioni possono ignorare questa classe o aggiungere un gestore di trasformazione post URL. Questo handler è utile quando l’applicazione desidera apportare modifiche alla richiesta URL dopo che è stata applicata la trasformazione predefinita.

* `PTNetworkConfiguration setURLTransformer:defaultTransformer` Metodo setter fornito sull’istanza di `PTNetworkConfiguration` metadati per impostare l’ `PTURLTransformer` implementazione.

>[!IMPORTANT]
>
>Le implementazioni dell&#39;app devono verificare la `PTURLTransformerInputType` enumerazione e trasformare solo gli URL di tipo `PTURLTransformerInputTypeCRSCreative` per CRS.

L&#39;esempio di codice seguente mostra come l&#39;applicazione può modificare il componente host predefinito in una stringa diversa (ad esempio, `cdn.mycrsdomain.com`):

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
