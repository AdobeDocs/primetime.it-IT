---
title: Implementare il supporto per i capitoli
description: Implementare il supporto per i capitoli
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '60'
ht-degree: 0%

---

# Implementare il supporto per i capitoli {#implement-chapter-support}

Puoi definire e tenere traccia di *personalizzato* capitoli per il tracciamento video nelle applicazioni basate su TVSDK.

I capitoli personalizzati vengono gestiti dall’applicazione e sono basati sui dati CMS o su un altro modo utilizzato dall’applicazione per definire i capitoli.

>[!CAUTION]
>
>I capitoli predefiniti non sono supportati in Android TVSDK 3.0.

Definisci e tieni traccia dei capitoli personalizzati.

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
