---
description: La classe di utilità TimeRangeCollection astratta il concetto di una raccolta ordinata di specifiche TimeRange e fornisce servizi per tradursi in un'istanza Metadata.
title: Classe TimeRangeCollection
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '70'
ht-degree: 0%

---


# Classe TimeRangeCollection{#timerangecollection-class}

La classe di utilità TimeRangeCollection astratta il concetto di una raccolta ordinata di specifiche TimeRange e fornisce servizi per tradursi in un&#39;istanza Metadata.

<!--<a id="section_D87AA7BC628D458DAB12D5247AD34B41"></a>-->

```
public final class TimeRangeCollection { 
    public static const MARK_RANGES:String = "mark_ranges"; 
  
    public function TimeRangeCollection(timeRanges:Vector.<TimeRange>) {…} 
    public function addTimeRange(timeRange:TimeRange):void {…} 
    public function toMetadata(options:Metadata):Metadata {…} 
}
```

Il valore definito per il tipo di raccolta è `MARK_RANGES`, `DELETE_RANGES` e `REPLACE_RANGES`. Puoi creare `TimeRangeCollection`s utilizzando questi tre tipi.
