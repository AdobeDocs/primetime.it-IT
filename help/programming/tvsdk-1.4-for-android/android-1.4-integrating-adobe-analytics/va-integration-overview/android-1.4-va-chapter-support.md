---
description: 'null'
seo-description: 'null'
seo-title: Implementare il supporto dei capitoli
title: Implementare il supporto dei capitoli
uuid: 5b39e494-85ad-43bb-ab56-a55797aa4ef7
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Implementare il supporto dei capitoli {#implement-chapter-support}

Potete definire e monitorare i capitoli per il tracciamento video in un’applicazione basata su TVSDK nei seguenti modi:

* Capitoli predefiniti, gestiti internamente da TVSDK.

   Un capitolo è definito come il tempo tra ciascuna interruzione di annuncio. Ad esempio, l’intervallo tra un annuncio pre-roll e il primo mid-roll è definito come il primo capitolo.
* Capitoli personalizzati, gestiti dall&#39;applicazione e basati sui dati CMS o su un altro modo utilizzato dall&#39;applicazione per definire i capitoli.

1. Definire e tenere traccia dei capitoli predefiniti o personalizzati.

   ```java
   // First, enable chapter tracking by setting  
   // the Boolean 'enableChapterTracking' to true: 
   
   vaMetadata.enableChapterTracking(true); 
   // For custom chapter definitions, provide an array list of chapters  
   // through the metadata. 
   // For example: 3 chapters of 60 second duration each 
   
   List<VideoAnalyticsChapterData> chapters = new ArrayList<VideoAnalyticsChapterData>(); 
   
   Int chapterDuration = 60; 
   for (var i = 0; i < 3; i++) { 
       VideoAnalyticsChapterData chapterData =  
         new VideoAnalyticsChapterData(i * chapterDuration, (i + 1) * chapterDuration);  
       chapterData.setName("chapter_" + (i+1)); 
       chapters.add(chapterData); 
   } 
   
   vaMetadata.setChapters(chapters); 
   // For default chapters, the application must not set  
   // custom chapters on the tracking metadata 
   // and simply enable chapters to be tracked by setting  
   // the boolean value as defined above.
   ```
