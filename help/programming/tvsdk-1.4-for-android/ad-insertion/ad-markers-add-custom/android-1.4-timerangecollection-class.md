---
description: La classe di utilità TimeRangeCollection illustra il concetto di una raccolta ordinata di specifiche TimeRange e fornisce servizi per la conversione di se stessa in un'istanza di metadati.
seo-description: La classe di utilità TimeRangeCollection illustra il concetto di una raccolta ordinata di specifiche TimeRange e fornisce servizi per la conversione di se stessa in un'istanza di metadati.
seo-title: TimeRangeCollection, classe
title: TimeRangeCollection, classe
uuid: 5705dc9d-4325-44b0-b5aa-196d09c3a67e
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 0%

---


# TimeRangeCollection, classe{#timerangecollection-class}

La classe di utilità TimeRangeCollection illustra il concetto di una raccolta ordinata di specifiche TimeRange e fornisce servizi per la conversione di se stessa in un&#39;istanza di metadati.

<!--<a id="section_D87AA7BC628D458DAB12D5247AD34B41"></a>-->

```java
public final class TimeRangeCollection {
    // default constructor method
    public TimeRangeCollection(Type type) {...}

    // the list of timerange specifications provided at construction time 
    public TimeRangeCollection(Type type, List<TimeRange> timeRanges) {...}

    // timerange specs can also be added later
    public void addTimeRange(TimeRange timeRange) {...}

    // translate the set of timerange specs into a Metadata instance 
    public Metadata toMetadata(Metadata options) {...}
}
```

Il parametro `type`, che è il primo parametro di posizione nella firma dei metodi del costruttore, è un&#39;istanza dell&#39;enumerazione `TimeRangeCollection#Type`. Fa parte della classe `TimeRangeCollection`. I valori attualmente definiti da questa enumerazione sono `MARK_RANGES`, `DELETE_RANGES` e `REPLACE_RANGES`. È possibile creare oggetti `TimeRangeCollection` utilizzando questi tre tipi.
