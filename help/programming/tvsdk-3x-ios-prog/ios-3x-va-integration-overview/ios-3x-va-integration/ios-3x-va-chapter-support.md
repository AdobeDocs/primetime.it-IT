---
title: Implementare il supporto per i capitoli
description: Implementare il supporto per i capitoli
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---


# Implementare il supporto per i capitoli {#implement-chapter-support}

Puoi definire e monitorare i capitoli per il tracciamento video in un’applicazione basata su TVSDK nei seguenti modi:

* Capitoli predefiniti, gestiti internamente da TVSDK.

   Un capitolo è definito come il tempo tra ciascuna interruzione pubblicitaria. Ad esempio, il tempo tra un annuncio pre-roll e il primo mid-roll è definito come il primo capitolo.
* Capitoli personalizzati, gestiti dall&#39;applicazione e basati sui dati CMS o in un altro modo che l&#39;applicazione utilizza per definire i capitoli.

   Definire e tenere traccia dei capitoli predefiniti o personalizzati.

   ```
   // First, enable chapter tracking by setting the boolean 'enableChapterTracking' to true: 
   
       vaTrackingMetadata.enableChapterTracking = YES; 
   
   // For custom chapter definitions, provide an array of chapters through the metadata:  
   // For example, 3 chapters of 60 second duration each: 
   
       NSMutableArray *chapters = [[[NSMutableArray alloc] init] autorelease]; 
   
       int chapterDuration = 60; 
       for (int i = 0; i < 3; i++) 
       { 
           PTVideoAnalyticsChapterData *chapterData =  
             [[[PTVideoAnalyticsChapterData alloc] init] autorelease]; 
           chapterData.name = [NSString stringWithFormat:@"chapter_%d", (i+1)]; 
           chapterData.range =  
             CMTimeRangeMake(CMTimeMakeWithSeconds(i * chapterDuration, 10000),  
             CMTimeMakeWithSeconds(chapterDuration, 10000)); 
   
           [chapters addObject:chapterData]; 
       } 
   
       vaTrackingMetadata.chapters = chapters; 
   
   // For default chapters, the application must not set custom chapters on the tracking metadata  
   // and simply enable chapters to be tracked by setting the boolean value as defined above.
   ```
