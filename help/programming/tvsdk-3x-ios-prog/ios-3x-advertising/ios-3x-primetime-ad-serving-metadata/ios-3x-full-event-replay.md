---
description: TVSDK supporta la risoluzione e l'inserimento di annunci per VOD e flussi live/lineari.
seo-description: TVSDK supporta la risoluzione e l'inserimento di annunci per VOD e flussi live/lineari.
seo-title: Primetime e metadati del server
title: Primetime e metadati del server
uuid: 61e224dd-551a-438f-8560-e64915087fef
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---


# Abilitare gli annunci nella riproduzione a tutti gli eventi {#section_6016E1DAF03645C8A8388D03C6AB7571}

La riproduzione a tutti gli eventi (FER) è una risorsa VOD che funge da risorsa live/DVR, pertanto l’applicazione deve adottare misure per garantire che gli annunci vengano inseriti correttamente.

Per i contenuti live, TVSDK utilizza i metadati/suggerimenti presenti nel manifesto per determinare dove inserire gli annunci. Tuttavia, a volte i contenuti live/lineari possono assomigliare ai contenuti VOD. Ad esempio, al termine del contenuto live, al manifesto live viene aggiunto un tag `EXT-X-ENDLIST`. Per HLS, il tag `EXT-X-ENDLIST` indica che il flusso è un flusso VOD. TVSDK non è in grado di distinguere automaticamente questo flusso da un normale flusso VOD per inserire correttamente gli annunci.

L&#39;applicazione deve indicare a TVSDK se il contenuto è live o VOD specificando il `PTAdSignalingMode`.

Per un flusso FER, il server di gestione annunci  Adobe Primetime non deve fornire l&#39;elenco delle interruzioni pubblicitarie che devono essere inserite nella timeline prima di avviare la riproduzione. Questo è il processo tipico per il contenuto VOD. Al contrario, specificando una diversa modalità di segnalazione, TVSDK legge tutti i cue point dal manifesto FER e va al server di annunci per ogni cue point per richiedere un&#39;interruzione annuncio. Questo processo è simile al contenuto live/DVR.

Oltre a ogni richiesta associata a un cue point, TVSDK invia una richiesta aggiuntiva per annunci pre-roll.

1. Da un&#39;origine esterna, come vCMS, ottenete la modalità di segnalazione da utilizzare.
1. Create i metadati relativi alla pubblicità.
1. Se il comportamento predefinito deve essere sovrascritto, specificare il `PTAdSignalingMode` utilizzando `PTAdMetadata.signalingMode`.

   I valori validi sono `PTAdSignalingModeDefault`, `PTAdSignalingModeManifestCues` e `PTAdSignalingModeServerMap`.

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
