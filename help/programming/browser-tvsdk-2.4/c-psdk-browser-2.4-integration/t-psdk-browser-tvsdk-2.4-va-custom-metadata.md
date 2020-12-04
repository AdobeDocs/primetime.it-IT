---
description: Potete fornire metadati personalizzati su contenuto, annunci e chiamate di tracciamento dei capitoli utilizzando le funzioni di callback.
seo-description: Potete fornire metadati personalizzati su contenuto, annunci e chiamate di tracciamento dei capitoli utilizzando le funzioni di callback.
seo-title: Implementazione del supporto dei metadati personalizzato
title: Implementazione del supporto dei metadati personalizzato
uuid: 6e23311c-a393-4485-919e-4cf6412789b1
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

