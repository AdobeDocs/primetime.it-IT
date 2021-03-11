---
description: TVSDK supporta la risoluzione e l’inserimento di annunci per VOD e flussi live/lineari.
title: Metadati di Primetime ad server
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 0%

---


# Abilitare gli annunci nella riproduzione completa degli eventi {#section_6016E1DAF03645C8A8388D03C6AB7571}

La riproduzione a eventi completi (FER) è una risorsa VOD che agisce come risorsa live/DVR, pertanto l’applicazione deve adottare misure per garantire che gli annunci siano posizionati correttamente.

Per i contenuti live, TVSDK utilizza i metadati/suggerimenti nel manifesto per determinare dove collocare gli annunci. Tuttavia, a volte i contenuti live/lineari potrebbero assomigliare al contenuto VOD. Ad esempio, al completamento del contenuto live, al manifesto live viene aggiunto un tag `EXT-X-ENDLIST` . Per HLS, il tag `EXT-X-ENDLIST` indica che il flusso è un flusso VOD. TVSDK non è in grado di distinguere automaticamente questo flusso da un normale flusso VOD per inserire correttamente gli annunci.

L’applicazione deve indicare a TVSDK se il contenuto è live o VOD specificando il `PTAdSignalingMode`.

Per un flusso FER, il server Adobe Primetime ad decisioning non deve fornire l&#39;elenco delle interruzioni pubblicitarie che devono essere inserite nella timeline prima di avviare la riproduzione. Questo è il processo tipico per il contenuto VOD. Invece, specificando una modalità di segnalazione diversa, TVSDK legge tutti i punti di cue dal manifesto FER e va al server di annunci per ogni punto di cue per richiedere un&#39;interruzione pubblicitaria. Questo processo è simile al contenuto live/DVR.

Oltre a ogni richiesta associata a un punto di cue, TVSDK invia una richiesta aggiuntiva di annunci per annunci pre-roll.

1. Da un&#39;origine esterna, ad esempio vCMS, ottenere la modalità di segnalazione da utilizzare.
1. Crea i metadati relativi alla pubblicità.
1. Se il comportamento predefinito deve essere sovrascritto, specifica `PTAdSignalingMode` utilizzando `PTAdMetadata.signalingMode`.

   I valori validi sono `PTAdSignalingModeDefault`, `PTAdSignalingModeManifestCues` e `PTAdSignalingModeServerMap`.

   È necessario impostare la modalità di segnalazione degli annunci prima di chiamare `prepareToPlay`. Dopo che TVSDK inizia a risolvere e posizionare gli annunci sulla timeline, le modifiche alla modalità di segnalazione degli annunci vengono ignorate. Imposta la modalità quando crei i metadati pubblicitari per la risorsa.

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
