---
description: 'null'
seo-description: 'null'
seo-title: Implementare il supporto dei capitoli
title: Implementare il supporto dei capitoli
uuid: 85d14b83-7910-4f5d-9ef2-511de916abd6
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d
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
   
       vaMetadata.enableChapterTracking = true; 
   
   // For custom chapter definitions, provide an array of chapters through the metadata:  
   // For example: 3 chapters of 60 second duration each 
   
       var chapters:Vector.<VideoAnalyticsChapterData> = new Vector.<VideoAnalyticsChapterData>(); 
       var chapterDuration:int = 60; 
       for (var i:int = 0; i < 3; i++) { 
           var chapterData:VideoAnalyticsChapterData =  
             new VideoAnalyticsChapterData(i * chapterDuration, (i + 1) * chapterDuration); 
           chapterData.name = "chapter_%d" + (i+1); 
   
           chapters.push(chapterData); 
       } 
   
       vaMetadata.chapters = chapters; 
   
   // For default chapters, the application must not set custom chapters on the tracking metadata  
   // and simply enable chapters to be tracked by setting the boolean value as defined above. 
   ```

