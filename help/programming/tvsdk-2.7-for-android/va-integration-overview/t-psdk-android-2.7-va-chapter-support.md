---
title: Implementare il supporto per i capitoli
description: Implementare il supporto per i capitoli
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '60'
ht-degree: 0%

---


# Implementare il supporto per i capitoli {#implement-chapter-support}

È possibile definire e tenere traccia dei capitoli *personalizzati* per il tracciamento video nelle applicazioni basate su TVSDK.

I capitoli personalizzati sono gestiti dall&#39;applicazione e si basano sui dati CMS o su un altro modo che l&#39;applicazione utilizza per definire i capitoli.

>[!CAUTION]
>
>I capitoli predefiniti non sono supportati in Android TVSDK 2.5.

1. Definire e tenere traccia dei capitoli personalizzati.

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

