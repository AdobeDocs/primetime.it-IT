---
description: La classe di utilità TimeRangeCollection astratta il concetto di una raccolta ordinata di specifiche TimeRange e fornisce servizi per tradursi in un'istanza Metadata.
title: Classe TimeRangeCollection
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---


# Classe TimeRangeCollection{#timerangecollection-class}

La classe di utilità TimeRangeCollection astratta il concetto di una raccolta ordinata di specifiche TimeRange e fornisce servizi per tradursi in un&#39;istanza Metadata.

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

Il parametro `type`, che è il primo parametro posizionale nella firma dei metodi del costruttore, è un&#39;istanza dell&#39;enumerazione `TimeRangeCollection#Type`. Fa parte della classe `TimeRangeCollection` . I valori attualmente definiti da questa enumerazione sono `MARK_RANGES`, `DELETE_RANGES` e `REPLACE_RANGES`. È possibile creare oggetti `TimeRangeCollection` utilizzando questi tre tipi.
