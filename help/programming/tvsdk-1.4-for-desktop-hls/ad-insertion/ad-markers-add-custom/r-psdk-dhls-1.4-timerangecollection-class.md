---
description: La classe di utilità TimeRangeCollection illustra il concetto di una raccolta ordinata di specifiche TimeRange e fornisce servizi per la conversione di se stessa in un'istanza di metadati.
seo-description: La classe di utilità TimeRangeCollection illustra il concetto di una raccolta ordinata di specifiche TimeRange e fornisce servizi per la conversione di se stessa in un'istanza di metadati.
seo-title: TimeRangeCollection, classe
title: TimeRangeCollection, classe
uuid: da781df4-6b19-47e1-8dc5-ea83c139f061
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# TimeRangeCollection, classe{#timerangecollection-class}

La classe di utilità TimeRangeCollection illustra il concetto di una raccolta ordinata di specifiche TimeRange e fornisce servizi per la conversione di se stessa in un&#39;istanza di metadati.

<!--<a id="section_D87AA7BC628D458DAB12D5247AD34B41"></a>-->

```
public final class TimeRangeCollection { 
    public static const MARK_RANGES:String = "mark_ranges"; 
  
    public function TimeRangeCollection(timeRanges:Vector.<TimeRange>) {…} 
    public function addTimeRange(timeRange:TimeRange):void {…} 
    public function toMetadata(options:Metadata):Metadata {…} 
}
```

Il valore definito per il tipo di raccolta è `MARK_RANGES`, `DELETE_RANGES`, e `REPLACE_RANGES`. Potete creare `TimeRangeCollection`questi tre tipi.
