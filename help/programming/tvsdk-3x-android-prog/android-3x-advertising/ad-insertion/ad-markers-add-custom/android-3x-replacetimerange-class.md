---
description: La classe dell'utilità ReplaceTimeRange è un'estensione della classe TimeRange da utilizzare con CustomRangeMetadata.
title: ReplaceTimeRange, classe
exl-id: 8d4e9263-bcc0-4300-86ac-6aa7afe5914b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '36'
ht-degree: 0%

---

# ReplaceTimeRange, classe {#replacetimerange-class}

La classe dell&#39;utilità ReplaceTimeRange è un&#39;estensione della classe TimeRange da utilizzare con CustomRangeMetadata.

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
