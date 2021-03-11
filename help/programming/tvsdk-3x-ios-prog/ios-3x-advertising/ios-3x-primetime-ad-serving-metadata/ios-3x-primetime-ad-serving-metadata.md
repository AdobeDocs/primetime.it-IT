---
description: TVSDK supporta la risoluzione e l’inserimento di annunci per VOD e flussi live/lineari.
title: Metadati di Primetime ad server
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---


# Panoramica {#primetime-ad-server-metadata-overview}

TVSDK supporta la risoluzione e l’inserimento di annunci per VOD e flussi live/lineari.

## Prerequisito

Prima di poter includere pubblicità nei contenuti video, fornisci le seguenti informazioni sui metadati:

* Un `mediaID` che identifica il contenuto specifico da riprodurre.
* Il tuo `zoneID`, che identifica la tua azienda o il tuo sito web.
* Il dominio del server di annunci, che specifica il dominio del server di annunci assegnato.
* Altri parametri di targeting.

## Configurare i metadati Primetime ad server {#section_86C4A3B2DF124770B9B7FD2511394313}

L’applicazione deve fornire a TVSDK le informazioni `PTAuditudeMetadata` necessarie per connettersi al server di annunci.

Per impostare i metadati del server di annunci:

1. Crea un&#39;istanza di [PTAuditudeMetadata](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAuditudeMetadata.html) e impostane le relative proprietà.

   ```
   PTAuditudeMetadata *adMetadata = [[PTAuditudeMetadata alloc] init];  
   adMetadata.zoneId = @"INSERT_YOUR_ZONE_ID_HERE"; 
   adMetadata.domain = @"INSERT_YOUR_DOMAIN_HERE"; 
   // Optionally set user agent 
   adMetadata.userAgent = @"INSERT_AGENT_NAME_HERE; 
   ```

1. Imposta l&#39;istanza `PTAuditudeMetadata` come metadati per i metadati correnti `PTMediaPlayerItem` utilizzando `PTAdResolvingMetadataKey`.

   ```
   // Metadata is an instance of PTMetadata that is used to create the PTMediaPlayerItem 
   [metadata setMetadata:adMetadata forKey:PTAdResolvingMetadataKey];  
   [adMetadata release];
   ```

   Ecco un esempio:

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
