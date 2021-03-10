---
description: La classe di utilità ReplaceTimeRange è un'estensione della classe TimeRange da utilizzare con CustomRangeMetadata.
title: ReplaceTimeRange, classe
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '36'
ht-degree: 0%

---


# Classe ReplaceTimeRange {#replacetimerange-class}

La classe di utilità ReplaceTimeRange è un&#39;estensione della classe TimeRange da utilizzare con CustomRangeMetadata.

```java
public class ReplaceTimeRange extends TimeRange {
    // Default constructor method
    public ReplaceTimeRange() { 
        ... 
    }

    // Details of begining, duration and replaceDuration 
    // provided at construction time 
    public ReplaceTimeRange(long begin, long duration, long replaceDuration) { 
        ... 
    }

    // Replace duration
    public long getReplaceDuration() { 
        ... 
    }
}
```

