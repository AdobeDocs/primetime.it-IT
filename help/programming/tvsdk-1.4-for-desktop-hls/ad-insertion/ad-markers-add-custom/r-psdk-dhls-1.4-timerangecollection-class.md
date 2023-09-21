---
description: La classe di utilità TimeRangeCollection astrae la nozione di insieme ordinato di specifiche TimeRange e fornisce servizi per tradursi in un'istanza di metadati.
title: Classe TimeRangeCollection
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '70'
ht-degree: 0%

---

# Classe TimeRangeCollection{#timerangecollection-class}

La classe di utilità TimeRangeCollection astrae la nozione di insieme ordinato di specifiche TimeRange e fornisce servizi per tradursi in un&#39;istanza di metadati.

<!--<a id="section_D87AA7BC628D458DAB12D5247AD34B41"></a>-->

```
public final class TimeRangeCollection { 
    public static const MARK_RANGES:String = "mark_ranges"; 
  
    public function TimeRangeCollection(timeRanges:Vector.<TimeRange>) {…} 
    public function addTimeRange(timeRange:TimeRange):void {…} 
    public function toMetadata(options:Metadata):Metadata {…} 
}
```

Il valore definito per il tipo di raccolta è `MARK_RANGES`, `DELETE_RANGES`, e `REPLACE_RANGES`. Puoi creare `TimeRangeCollection`utilizza questi tre tipi.
