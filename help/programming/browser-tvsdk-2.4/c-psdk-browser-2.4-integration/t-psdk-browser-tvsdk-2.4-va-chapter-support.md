---
description: 'null'
seo-description: 'null'
seo-title: Implementare il supporto dei capitoli
title: Implementare il supporto dei capitoli
uuid: 70f10621-febe-4443-84e7-ce95bec53377
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Implementare il supporto dei capitoli{#implement-chapter-support}

Un capitolo è definito come il tempo tra ciascuna interruzione di annuncio. Ad esempio, l’intervallo tra un annuncio pre-roll e il primo mid-roll è definito come il primo capitolo. Potete definire e tenere traccia dei capitoli per il tracciamento video in un’applicazione basata su browser TVSDK utilizzando capitoli personalizzati. I capitoli personalizzati sono gestiti dall&#39;applicazione e si basano sui dati CMS o su un altro modo utilizzato dall&#39;applicazione per definire i capitoli.

1. Definizione e tracciamento di capitoli personalizzati.

   ```js
   vaObj.enableChapterTracking = true; 
   
   // For custom chapter definitions, provide an array of chapters through the metadata: 
   // For example: 3 chapters of 60 second duration each 
   var chapters = []; 
   var chapterDuration = 60; 
   for (var i = 0; i < 3; i++) { 
       var chapterData = new AdobePSDK.VA.VideoAnalyticsChapterData("chapter_" + (i+1), i * chapterDuration, chapterDuration, (i+1)); 
       chapters.push(chapterData); 
   } 
   
   vaObj.chapters = chapters;
   ```

