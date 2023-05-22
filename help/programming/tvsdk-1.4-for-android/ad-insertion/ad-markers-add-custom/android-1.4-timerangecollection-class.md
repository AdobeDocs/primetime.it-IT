---
description: La classe di utilità TimeRangeCollection astrae la nozione di insieme ordinato di specifiche TimeRange e fornisce servizi per tradursi in un'istanza di metadati.
title: Classe TimeRangeCollection
exl-id: 1af41267-c222-43ac-84ca-0bf37b6a59de
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---

# Classe TimeRangeCollection{#timerangecollection-class}

La classe di utilità TimeRangeCollection astrae la nozione di insieme ordinato di specifiche TimeRange e fornisce servizi per tradursi in un&#39;istanza di metadati.

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

Il `type` Il parametro, che è il primo parametro posizionale nella firma dei metodi di costruzione, è un&#39;istanza di `TimeRangeCollection#Type` enumerazione. Questo fa parte del `TimeRangeCollection` classe. I valori attualmente definiti da questa enumerazione sono `MARK_RANGES`, `DELETE_RANGES`, e `REPLACE_RANGES`. Puoi creare `TimeRangeCollection` che utilizzano questi tre tipi.
