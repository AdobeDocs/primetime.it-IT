---
description: È possibile utilizzare più resolver di contenuti per gestire diverse operazioni della timeline.
title: Risolutori di contenuti per cancellazione/sostituzione di annunci
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '34'
ht-degree: 0%

---


# Risolutori di contenuti per eliminazione/sostituzione di annunci {#content-resolvers-for-ad-deletion-replacement}

È possibile utilizzare più resolver di contenuti per gestire diverse operazioni della timeline.

```java
List<ContentResolver> contentResolvers = new ArrayList<ContentResolver>(); 
MetadataNode metadata = (MetadataNode) resource.getMetadata(); 
if (metadata != null) { 
    if (metadata.containsKey(DefaultMetadataKeys.TIME_RANGES_METADATA_KEY.getValue())) { 
        String timeRangeType = metadata.getValue(DefaultMetadataKeys.TIME_RANGES_METADATA_KEY.getValue()); 
        if (timeRangeType.equals(TimeRangeCollection.TIME_RANGE_TYPE_DELETE)) { 
            contentResolvers.add(new DeleteContentResolver()); 
        } else if (timeRangeType.equals(TimeRangeCollection.TIME_RANGE_TYPE_REPLACE)) { 
            contentResolvers.add(new DeleteContentResolver()); 
        } else if (timeRangeType.equals(TimeRangeCollection.TIME_RANGE_TYPE_MARK)) { 
            contentResolvers.add(new CustomAdMarkersContentResolver()); 
        } 
    } 
    if (metadata.containsKey(DefaultMetadataKeys.AUDITUDE_METADATA_KEY.getValue())) { 
        contentResolvers.add(new AuditudeResolver(context)); 
    } else if (metadata.containsKey(DefaultMetadataKeys.JSON_METADATA_KEY.getValue())) { 
        contentResolvers.add(new MetadataResolver()); 
    } 
} 
return contentResolvers;
```

