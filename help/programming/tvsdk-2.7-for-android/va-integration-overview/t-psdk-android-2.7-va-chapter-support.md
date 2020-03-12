---
description: 'null'
seo-description: 'null'
seo-title: Implementare il supporto dei capitoli
title: Implementare il supporto dei capitoli
uuid: f62a8244-6393-4a38-9ae2-8ac31f6a8a06
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Implementare il supporto dei capitoli {#implement-chapter-support}

Potete definire e monitorare capitoli *personalizzati* per il tracciamento video nelle applicazioni basate su TVSDK.

I capitoli personalizzati sono gestiti dall&#39;applicazione e si basano sui dati CMS o su un altro modo utilizzato dall&#39;applicazione per definire i capitoli.

>[!CAUTION]
>
>I capitoli predefiniti non sono supportati in Android TVSDK 2.5.

1. Definizione e tracciamento di capitoli personalizzati.

   ```java
   // First, enable chapter tracking by setting   
   // enableChapterTracking to true: 
   
   vaMetadata.enableChapterTracking(true); 
   // For custom chapter definitions, provide  
   // an array list of chapters through the metadata. 
   // For example: 3 chapters of 60 second duration each 
   
   List<VideoAnalyticsChapterData> chapters =  
     new ArrayList<VideoAnalyticsChapterData>(); 
   
   Int chapterDuration = 60; 
   for (var i = 0; i < 3; i++) { 
       VideoAnalyticsChapterData chapterData =  
         new VideoAnalyticsChapterData(i * chapterDuration, (i + 1) * chapterDuration);  
       chapterData.setName("chapter_" + (i+1)); 
       chapters.add(chapterData); 
   } 
   
   vaMetadata.setChapters(chapters); 
   ```

