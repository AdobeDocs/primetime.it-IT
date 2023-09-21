---
description: I marcatori di annunci personalizzati ti consentono di trasmettere a TVSDK un set di specifiche TimeRange che rappresentano i segmenti della timeline.
title: TimeRange, classe
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---

# TimeRange, classe{#timerange-class}

I marcatori di annunci personalizzati ti consentono di trasmettere a TVSDK un set di specifiche TimeRange che rappresentano i segmenti della timeline.

<!--<a id="section_42EB6D62627A424ABA250E3246EFEFC3"></a>-->

Ogni `TimeRange` La specifica nel set rappresenta un segmento nella timeline di riproduzione gestito internamente da TVSDK e che deve essere contrassegnato in modo appropriato come periodo relativo agli annunci.

Il `TimeRange` La classe è una semplice struttura di dati che espone la posizione iniziale e finale sulla timeline. Queste due proprietà di sola lettura astraggono l’idea di un intervallo di tempo nella timeline di riproduzione.

>[!TIP]
>
>Entrambi i valori sono espressi in millisecondi.

Riepilogo della classe TimeRange:

```
public final class TimeRange {
    // the start/end values are provided at construction 
    public static function createRange(begin:Number, duration:Number {…}
 
    public function get begin():Number {…}
    public function get end():Number {…}
    public function get duration():Number {…}
}
```
