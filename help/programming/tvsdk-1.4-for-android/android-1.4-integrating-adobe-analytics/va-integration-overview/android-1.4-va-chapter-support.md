---
title: Implementare il supporto per i capitoli
description: Implementare il supporto per i capitoli
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---

# Implementare il supporto per i capitoli {#implement-chapter-support}

Puoi definire e tenere traccia dei capitoli per il tracciamento video in un’applicazione basata su TVSDK nei seguenti modi:

* Capitoli predefiniti, gestiti internamente da TVSDK.

  Un capitolo è definito come il tempo tra ogni interruzione pubblicitaria. Ad esempio, il tempo tra un’interruzione pubblicitaria pre-roll e il primo mid-roll è definito come primo capitolo.
* Capitoli personalizzati, gestiti dall’applicazione e basati su dati CMS o in un altro modo utilizzato dall’applicazione per definire i capitoli.

1. Definisci e tieni traccia dei capitoli predefiniti o personalizzati.

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
