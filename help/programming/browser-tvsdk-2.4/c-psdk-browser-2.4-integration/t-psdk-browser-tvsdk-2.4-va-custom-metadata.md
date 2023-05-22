---
description: Puoi fornire metadati personalizzati su contenuti, annunci e chiamate di tracciamento dei capitoli utilizzando funzioni di callback.
title: Implementazione del supporto per metadati personalizzati
exl-id: d2291649-79e2-4935-8980-4f2038d58342
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '74'
ht-degree: 0%

---

# Implementazione del supporto per metadati personalizzati{#implement-custom-metadata-support}

Puoi fornire metadati personalizzati su contenuti, annunci e chiamate di tracciamento dei capitoli utilizzando funzioni di callback.

Le funzioni di callback vengono richiamate immediatamente prima della chiamata di tracciamento, in modo che l’applicazione possa allegare i metadati specifici di un annuncio o di un capitolo.

1. Richiama le funzioni di callback per contenuto, annunci e capitoli.

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
