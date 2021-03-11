---
description: Puoi fornire metadati personalizzati su contenuti, annunci e chiamate di tracciamento dei capitoli utilizzando le funzioni di callback.
title: Implementazione del supporto per metadati personalizzati
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '74'
ht-degree: 0%

---


# Implementare il supporto per i metadati personalizzati{#implement-custom-metadata-support}

Puoi fornire metadati personalizzati su contenuti, annunci e chiamate di tracciamento dei capitoli utilizzando le funzioni di callback.

Le funzioni di callback vengono richiamate immediatamente prima della chiamata di tracciamento, in modo che l&#39;applicazione possa allegare i metadati specifici di un annuncio o di un capitolo.

1. Richiama le funzioni di callback per contenuti, annunci pubblicitari e capitoli.

   ```js
   vaObj.videoMetadataBlock = function() { 
       return { 
           "name" : "my-video", 
           "genre" : "comedy" 
       }; 
   } 
   
   vaObj.adMetadataBlock = function(ad) { 
       return { 
           "name" : "my-ad", 
           "category" : "automotive" 
       }; 
   } 
   
   vaObj.chapterMetadataBlock = function(chapter) { 
       return { 
           "name" : "my-chapter", 
           "type" : "quartile" 
       }; 
   }
   ```

