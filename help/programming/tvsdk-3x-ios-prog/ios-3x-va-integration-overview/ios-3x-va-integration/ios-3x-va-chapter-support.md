---
description: 'null'
seo-description: 'null'
seo-title: Implementare il supporto dei capitoli
title: Implementare il supporto dei capitoli
uuid: b0e5ef1c-6568-4901-9ac7-261df71a0110
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---


# Implementare il supporto dei capitoli {#implement-chapter-support}

Potete definire e monitorare i capitoli per il tracciamento video in un’applicazione basata su TVSDK nei seguenti modi:

* Capitoli predefiniti, gestiti internamente da TVSDK.

   Un capitolo è definito come il tempo tra ciascuna interruzione di annuncio. Ad esempio, l’intervallo tra un annuncio pre-roll e il primo mid-roll è definito come il primo capitolo.
* Capitoli personalizzati, gestiti dall&#39;applicazione e basati sui dati CMS o su un altro modo utilizzato dall&#39;applicazione per definire i capitoli.

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
