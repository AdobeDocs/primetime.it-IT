---
description: TVSDK supporta la risoluzione e l'inserimento di annunci per VOD e flussi live/lineari.
seo-description: TVSDK supporta la risoluzione e l'inserimento di annunci per VOD e flussi live/lineari.
seo-title: Primetime e metadati del server
title: Primetime e metadati del server
uuid: 61e224dd-551a-438f-8560-e64915087fef
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# Panoramica {#primetime-ad-server-metadata-overview}

TVSDK supporta la risoluzione e l&#39;inserimento di annunci per VOD e flussi live/lineari.

[!PREREQUISITE] {othertype=&quot;Prequisite&quot;}

Prima di includere la pubblicità nei contenuti video, fornite le seguenti informazioni sui metadati:

* A `mediaID`, che identifica il contenuto specifico da riprodurre.
* Il vostro `zoneID`, che identifica la vostra società o il vostro sito Web.
* Il dominio del server di annunci, che specifica il dominio del server di annunci assegnato.
* Altri parametri di targeting.

## Configurare i metadati Primetime e del server {#section_86C4A3B2DF124770B9B7FD2511394313}

L’applicazione deve fornire a TVSDK le `PTAuditudeMetadata` informazioni necessarie per connettersi al server degli annunci.

Per impostare i metadati del server di annunci:

1. Create un’istanza di [PTAuditudeMetadata](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAuditudeMetadata.html) e impostatene le proprietà.

   ```
   PTAuditudeMetadata *adMetadata = [[PTAuditudeMetadata alloc] init];  
   adMetadata.zoneId = @"INSERT_YOUR_ZONE_ID_HERE"; 
   adMetadata.domain = @"INSERT_YOUR_DOMAIN_HERE"; 
   // Optionally set user agent 
   adMetadata.userAgent = @"INSERT_AGENT_NAME_HERE; 
   ```

1. Impostate l&#39; `PTAuditudeMetadata` istanza come metadati per i `PTMediaPlayerItem` metadati correnti utilizzando `PTAdResolvingMetadataKey`.

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
