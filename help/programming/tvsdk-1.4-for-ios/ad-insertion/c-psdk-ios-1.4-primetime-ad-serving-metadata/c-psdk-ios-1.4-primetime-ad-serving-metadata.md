---
description: TVSDK supporta la risoluzione e l'inserimento di annunci per VOD e flussi live/lineari.
seo-description: TVSDK supporta la risoluzione e l'inserimento di annunci per VOD e flussi live/lineari.
seo-title: Primetime e metadati del server
title: Primetime e metadati del server
uuid: 314f14c0-4da4-4da6-96f9-5a5ffea22a99
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Panoramica {#primetime-ad-server-metadata-overview}

TVSDK supporta la risoluzione e l&#39;inserimento di annunci per VOD e flussi live/lineari.

>[!NOTE] {othertype=&quot;Prequisite&quot;}
>
>Prima di includere la pubblicità nei contenuti video, fornite le seguenti informazioni sui metadati:
>
>* A `mediaID`, che identifica il contenuto specifico da riprodurre.
>* Il vostro `zoneID`, che identifica la vostra società o il vostro sito Web.
>* Il dominio del server di annunci, che specifica il dominio del server di annunci assegnato.
>* Altri parametri di targeting.
>



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

## Abilitare gli annunci nella riproduzione a tutti gli eventi {#section_6016E1DAF03645C8A8388D03C6AB7571}

La riproduzione a tutti gli eventi (FER) è una risorsa VOD che funge da risorsa live/DVR, pertanto l’applicazione deve adottare misure per garantire che gli annunci vengano inseriti correttamente.

Per i contenuti live, TVSDK utilizza i metadati/suggerimenti presenti nel manifesto per determinare dove inserire gli annunci. Tuttavia, a volte i contenuti live/lineari possono assomigliare ai contenuti VOD. Ad esempio, al termine del contenuto live, al manifesto attivo viene aggiunto un `EXT-X-ENDLIST` tag. Per HLS, il `EXT-X-ENDLIST` tag indica che il flusso è un flusso VOD. TVSDK non è in grado di distinguere automaticamente questo flusso da un normale flusso VOD per inserire correttamente gli annunci.

L’applicazione deve indicare a TVSDK se il contenuto è live o VOD specificando il `PTAdSignalingMode`.

Per un flusso FER, il server Adobe Primetime ad Decioning non deve fornire l&#39;elenco delle interruzioni pubblicitarie che devono essere inserite nella timeline prima di avviare la riproduzione. Questo è il processo tipico per il contenuto VOD. Al contrario, specificando una diversa modalità di segnalazione, TVSDK legge tutti i cue point dal manifesto FER e va al server di annunci per ogni cue point per richiedere un&#39;interruzione annuncio. Questo processo è simile al contenuto live/DVR.

Oltre a ogni richiesta associata a un cue point, TVSDK invia una richiesta aggiuntiva per annunci pre-roll.

1. Da un&#39;origine esterna, come vCMS, ottenete la modalità di segnalazione da utilizzare.
1. Create i metadati relativi alla pubblicità.
1. Se il comportamento predefinito deve essere sovrascritto, specificatelo `PTAdSignalingMode` utilizzando `PTAdMetadata.signalingMode`.

   I valori validi sono `PTAdSignalingModeDefault`, `PTAdSignalingModeManifestCues`, e `PTAdSignalingModeServerMap`.

   È necessario impostare la modalità di segnalazione degli annunci prima di chiamare `prepareToPlay`. Dopo che TVSDK ha iniziato a risolvere e inserire gli annunci sulla timeline, le modifiche alla modalità di segnalazione degli annunci vengono ignorate. Impostate la modalità quando create i metadati pubblicitari per la risorsa.

1. Continua a riprodurre.

   ```
      PTMetadata *metadata = [[[PTMetadata alloc] init] autorelease]; 
   PTAuditudeMetadata *adMetadata = [[[PTAuditudeMetadata alloc] init] autorelease]; 
   adMetadata.zoneId = your-auditude-zone-id; 
   adMetadata.domain = @"your-auditude-domain"; 
   //adMetadata.enableDVRAds = YES; // FOR LIVE DVR case 
   //adMetadata.signalingMode = PTAdSignalingModeManifestCues;  
   // FOR VOD FER case 
   NSMutableDictionary *targetingParameters = [[[NSMutableDictionary alloc] init] autorelease]; 
   [targetingParameters setValue:@"ipad" forKey:@"device"]; 
   [targetingParameters setValue:@"preroll" forKey:@"AD_OPPORTUNITY_ID"]; 
   adMetadata.targetingParameters = targetingParameters; 
   NSMutableDictionary *customParameters = [[[NSMutableDictionary alloc] init] autorelease]; 
   [customParameters setValue:@"your-media-id" forKey:@"NW_ID"]; 
   [customParameters setValue:@"preroll" forKey:@"AD_OPPORTUNITY_ID"]; 
   adMetadata.customParameters = customParameters; 
   [metadata setMetadata:adMetadata forKey:PTAdResolvingMetadataKey]; 
   ```

