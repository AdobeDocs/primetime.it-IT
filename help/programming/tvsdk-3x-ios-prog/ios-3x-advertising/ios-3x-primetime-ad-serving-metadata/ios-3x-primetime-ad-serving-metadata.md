---
description: TVSDK supporta la risoluzione e l’inserimento di annunci per flussi VOD e live/lineari.
title: Metadati di Primetime ad server
exl-id: f27657ac-4037-45e5-a658-ad9a783dd990
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---

# Panoramica {#primetime-ad-server-metadata-overview}

TVSDK supporta la risoluzione e l’inserimento di annunci per flussi VOD e live/lineari.

## Prerequisito

Prima di poter includere la pubblicità nel contenuto video, fornisci le seguenti informazioni sui metadati:

* A `mediaID`, che identifica il contenuto specifico da riprodurre.
* Il tuo `zoneID`, che identifica l&#39;azienda o il sito Web.
* Il dominio dell’ad server, che specifica il dominio dell’ad server assegnato.
* Altri parametri di targeting.

## Configurare i metadati di Primetime ad server {#section_86C4A3B2DF124770B9B7FD2511394313}

L&#39;applicazione deve fornire a TVSDK i `PTAuditudeMetadata` informazioni per la connessione al server di annunci.

Per impostare i metadati dell&#39;ad server:

1. Crea un&#39;istanza di [PTAuditudeMetadata](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAuditudeMetadata.html) e impostarne le proprietà.

   ```
   PTAuditudeMetadata *adMetadata = [[PTAuditudeMetadata alloc] init];  
   adMetadata.zoneId = @"INSERT_YOUR_ZONE_ID_HERE"; 
   adMetadata.domain = @"INSERT_YOUR_DOMAIN_HERE"; 
   // Optionally set user agent 
   adMetadata.userAgent = @"INSERT_AGENT_NAME_HERE; 
   ```

1. Imposta il `PTAuditudeMetadata` come metadati per l’istanza corrente `PTMediaPlayerItem` metadati tramite `PTAdResolvingMetadataKey`.

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
