---
title: Implementare il supporto per i capitoli
description: Implementare il supporto per i capitoli
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '84'
ht-degree: 0%

---


# Implementa il supporto per i capitoli{#implement-chapter-support}

Un capitolo è definito come il tempo tra ciascuna interruzione pubblicitaria. Ad esempio, il tempo tra un annuncio pre-roll e il primo mid-roll è definito come il primo capitolo. Puoi definire e monitorare i capitoli per il tracciamento video in un’applicazione basata su browser TVSDK utilizzando capitoli personalizzati. I capitoli personalizzati sono gestiti dall&#39;applicazione e si basano sui dati CMS o su un altro modo che l&#39;applicazione utilizza per definire i capitoli.

1. Definire e tenere traccia dei capitoli personalizzati.

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

