---
description: TVSDK supporta la risoluzione e l'inserimento di annunci per VOD e flussi live/lineari.
seo-description: TVSDK supporta la risoluzione e l'inserimento di annunci per VOD e flussi live/lineari.
seo-title: Primetime e metadati del server
title: Primetime e metadati del server
uuid: 61e224dd-551a-438f-8560-e64915087fef
translation-type: tm+mt
source-git-commit: 9d60bff4035963572e49fa49effa576ca854f799
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 0%

---


# Panoramica {#primetime-ad-server-metadata-overview}

TVSDK supporta la risoluzione e l&#39;inserimento di annunci per VOD e flussi live/lineari.

## Prerequisito

Prima di includere la pubblicità nei contenuti video, fornite le seguenti informazioni sui metadati:

* Un `mediaID` che identifica il contenuto specifico da riprodurre.
* `zoneID`, che identifica la società o il sito Web.
* Il dominio del server di annunci, che specifica il dominio del server di annunci assegnato.
* Altri parametri di targeting.

## Impostare i metadati di Primetime ad server {#section_86C4A3B2DF124770B9B7FD2511394313}

L&#39;applicazione deve fornire a TVSDK le informazioni `PTAuditudeMetadata` necessarie per connettersi al server di annunci.

Per impostare i metadati del server di annunci:

1. Create un&#39;istanza di [PTAuditudeMetadata](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAuditudeMetadata.html) e impostatene le proprietà.

   ```
   PTAuditudeMetadata *adMetadata = [[PTAuditudeMetadata alloc] init];  
   adMetadata.zoneId = @"INSERT_YOUR_ZONE_ID_HERE"; 
   adMetadata.domain = @"INSERT_YOUR_DOMAIN_HERE"; 
   // Optionally set user agent 
   adMetadata.userAgent = @"INSERT_AGENT_NAME_HERE; 
   ```

1. Impostate l&#39;istanza `PTAuditudeMetadata` come metadati per i metadati correnti `PTMediaPlayerItem` utilizzando `PTAdResolvingMetadataKey`.

   ```
   // Metadata is an instance of PTMetadata that is used to create the PTMediaPlayerItem 
   [metadata setMetadata:adMetadata forKey:PTAdResolvingMetadataKey];  
   [adMetadata release];
   ```

   Esempio:

   ```
   PTMetadata *metadata = [self createMetadata]; 
   PTMediaPlayerItem *item =  
     [[[PTMediaPlayerItem alloc] initWithUrl:url mediaId:yourMediaID metadata:metadata] autorelease]; 
   
   - (PTMetadata *) createMetadata { 
       PTMetadata* metadata = [[[PTMetadata alloc] init] autorelease]; 
   
       PTAuditudeMetadata *adMetadata = [[[PTAuditudeMetadata alloc] init] autorelease];  
       adMetadata.zoneId = yourZoneID; 
       adMetadata.domain = yourAdServerDomain; 
   
       [metadata setMetadata:adMetadata forKey:PTAdResolvingMetadataKey]; 
   
       return metadata; 
   }
   ```
