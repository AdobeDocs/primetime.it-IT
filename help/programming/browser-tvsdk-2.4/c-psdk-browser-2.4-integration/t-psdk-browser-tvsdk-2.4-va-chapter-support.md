---
title: Implementare il supporto per i capitoli
description: Implementare il supporto per i capitoli
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '84'
ht-degree: 0%

---

# Implementare il supporto per i capitoli{#implement-chapter-support}

Un capitolo è definito come il tempo tra ogni interruzione pubblicitaria. Ad esempio, il tempo tra un’interruzione pubblicitaria pre-roll e il primo mid-roll è definito come primo capitolo. Puoi definire e tenere traccia dei capitoli per il tracciamento video in un’applicazione basata su TVSDK per browser utilizzando capitoli personalizzati. I capitoli personalizzati vengono gestiti dall’applicazione e sono basati sui dati CMS o su un altro modo utilizzato dall’applicazione per definire i capitoli.

1. Definisci e tieni traccia dei capitoli personalizzati.

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
