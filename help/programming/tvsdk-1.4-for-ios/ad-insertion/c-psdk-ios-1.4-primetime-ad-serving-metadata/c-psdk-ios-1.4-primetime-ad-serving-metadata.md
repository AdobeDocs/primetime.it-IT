---
description: TVSDK supporta la risoluzione e l’inserimento di annunci per flussi VOD e live/lineari.
title: Metadati di Primetime ad server
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 0%

---

# Panoramica {#primetime-ad-server-metadata-overview}

TVSDK supporta la risoluzione e l’inserimento di annunci per flussi VOD e live/lineari.

>[!NOTE]
>
>Prima di poter includere la pubblicità nel contenuto video, fornisci le seguenti informazioni sui metadati:
>
>* A `mediaID`, che identifica il contenuto specifico da riprodurre.
>* Il tuo `zoneID`, che identifica l&#39;azienda o il sito Web.
>* Il dominio dell’ad server, che specifica il dominio dell’ad server assegnato.
>* Altri parametri di targeting.
>

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

## Abilitare gli annunci nella riproduzione completa degli eventi {#section_6016E1DAF03645C8A8388D03C6AB7571}

La riproduzione completa degli eventi (FER) è una risorsa VOD che funge da risorsa live/DVR, pertanto l’applicazione deve adottare misure per garantire che gli annunci vengano inseriti correttamente.

Per il contenuto live, TVSDK utilizza i metadati/suggerimenti nel manifesto per determinare dove inserire gli annunci. Tuttavia, a volte i contenuti live/lineari possono assomigliare ai contenuti VOD. Ad esempio, al termine del contenuto live, un `EXT-X-ENDLIST` viene aggiunto al manifesto live. Per HLS, `EXT-X-ENDLIST` tag significa che il flusso è un flusso VOD. TVSDK non può distinguere automaticamente questo flusso da un normale flusso VOD per inserire correttamente gli annunci.

L&#39;applicazione deve comunicare a TVSDK se il contenuto è live o VOD specificando `PTAdSignalingMode`.

Per un flusso FER, il server Adobe Primetime ad decisioning non deve fornire l’elenco delle interruzioni pubblicitarie che devono essere inserite nella timeline prima di avviare la riproduzione. Questo è il processo tipico per il contenuto VOD. Specificando invece una modalità di segnalazione diversa, TVSDK legge tutti i cue point dal manifesto FER e va all’ad server per ogni cue point per richiedere un’interruzione pubblicitaria. Questo processo è simile al contenuto live/DVR.

Oltre a ogni richiesta associata a un cue point, TVSDK effettua un’ulteriore richiesta di annuncio per gli annunci pre-roll.

1. Da un&#39;origine esterna, ad esempio vCMS, ottenere la modalità di segnalazione da utilizzare.
1. Crea i metadati relativi alla pubblicità.
1. Se il comportamento predefinito deve essere sovrascritto, specifica `PTAdSignalingMode` utilizzando `PTAdMetadata.signalingMode`.

   I valori validi sono `PTAdSignalingModeDefault`, `PTAdSignalingModeManifestCues`, e `PTAdSignalingModeServerMap`.

   È necessario impostare la modalità di segnalazione dell’annuncio prima di richiamare `prepareToPlay`. Una volta che TVSDK inizia a risolvere e a posizionare gli annunci sulla timeline, le modifiche alla modalità di segnalazione degli annunci vengono ignorate. Imposta la modalità quando crei i metadati pubblicitari per la risorsa.

1. Continuare la riproduzione.

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
