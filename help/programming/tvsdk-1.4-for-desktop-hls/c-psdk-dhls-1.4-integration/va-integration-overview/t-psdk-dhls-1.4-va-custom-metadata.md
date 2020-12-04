---
description: Potete fornire metadati personalizzati su contenuto, annunci e chiamate di tracciamento dei capitoli utilizzando le funzioni di callback.
seo-description: Potete fornire metadati personalizzati su contenuto, annunci e chiamate di tracciamento dei capitoli utilizzando le funzioni di callback.
seo-title: Implementazione del supporto dei metadati personalizzato
title: Implementazione del supporto dei metadati personalizzato
uuid: 2186db58-10b0-43a6-840f-53ab289843ee
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 0%

---


# Implementare il supporto dei metadati personalizzato{#implement-custom-metadata-support}

Potete fornire metadati personalizzati su contenuto, annunci e chiamate di tracciamento dei capitoli utilizzando le funzioni di callback.

Le funzioni di callback vengono richiamate immediatamente prima della chiamata di tracciamento, in modo che l’applicazione possa allegare i metadati specifici di un annuncio o di un capitolo.

1. Richiama le funzioni di callback per contenuto, annunci pubblicitari e capitoli.

   ```
   // Video Metadata Block 
   vaMetadata.videoMetadataBlock = function():Object { 
       return {"myvideoid":"1234", "mysdkversion":Version.version} 
   }; 
   
   // Ad Metadata Block invoked on every ad start 
   vaMetadata.adMetadataBlock = function(ad:Ad):Object { 
       return {"myadid":"ad-1234", "myad-sdkversion":Version.version} 
   }; 
   
   // Chapter Metadata Block invoked on every chapter start 
   vaMetadata.chapterMetadataBlock = function(chapter:VideoAnalyticsChapterData) { 
       return {"mychapterid":"chapter-1234", "mychapter-sdkversion":Version.version} 
   };
   ```

