---
description: Puoi fornire metadati personalizzati su contenuti, annunci e chiamate di tracciamento dei capitoli utilizzando funzioni di callback.
title: Implementazione del supporto per metadati personalizzati
exl-id: c7478578-7f49-4fd0-b381-c558888401aa
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '74'
ht-degree: 0%

---

# Implementazione del supporto per metadati personalizzati{#implement-custom-metadata-support}

Puoi fornire metadati personalizzati su contenuti, annunci e chiamate di tracciamento dei capitoli utilizzando funzioni di callback.

Le funzioni di callback vengono richiamate immediatamente prima della chiamata di tracciamento, in modo che l’applicazione possa allegare i metadati specifici di un annuncio o di un capitolo.

Richiama le funzioni di callback per contenuto, annunci e capitoli.

```
// Video Metadata Block 
    vaTrackingMetadata.videoMetadataBlock = ^NSDictionary *() 
    { 
        return @{ 
                 @"myvideoid": @"1234", 
                 @"mysdkversion": [PTSDK apiVersion] 
                 }; 
    }; 
      
// Ad Metadata Block invoked on every ad start 
    vaTrackingMetadata.adMetadataBlock = ^NSDictionary *(PTAd *ad) 
    { 
        return @{ 
                 @"myadid": @"ad-1234", 
                 @"myad-sdkversion": [PTSDK apiVersion] 
                 }; 
    }; 
      
// Chapter Metadata Block invoked on every chapter start 
    vaTrackingMetadata.chapterMetadataBlock = ^NSDictionary *(PTVideoAnalyticsChapterData *chapter) 
    { 
        return @{ 
                 @"mychapterid": @"chapter-1234", 
                 @"mychapter-sdkversion": [PTSDK apiVersion] 
                 }; 
    };
```
