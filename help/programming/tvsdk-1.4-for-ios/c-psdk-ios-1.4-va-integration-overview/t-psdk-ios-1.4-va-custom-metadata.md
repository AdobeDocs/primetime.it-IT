---
description: Potete fornire metadati personalizzati su contenuto, annunci e chiamate di tracciamento dei capitoli utilizzando le funzioni di callback.
seo-description: Potete fornire metadati personalizzati su contenuto, annunci e chiamate di tracciamento dei capitoli utilizzando le funzioni di callback.
seo-title: Implementazione del supporto dei metadati personalizzato
title: Implementazione del supporto dei metadati personalizzato
uuid: eb8d383f-a3e8-402d-84e8-f4209df0f954
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 0%

---


# Implementare il supporto dei metadati personalizzato{#implement-custom-metadata-support}

Potete fornire metadati personalizzati su contenuto, annunci e chiamate di tracciamento dei capitoli utilizzando le funzioni di callback.

Le funzioni di callback vengono richiamate immediatamente prima della chiamata di tracciamento, in modo che l’applicazione possa allegare i metadati specifici di un annuncio o di un capitolo.

Richiama le funzioni di callback per contenuto, annunci pubblicitari e capitoli.

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

