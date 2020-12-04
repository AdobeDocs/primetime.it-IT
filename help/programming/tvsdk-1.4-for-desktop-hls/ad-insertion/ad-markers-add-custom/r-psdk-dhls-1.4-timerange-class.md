---
description: I marcatori di annunci personalizzati consentono di passare una serie di specifiche TimeRange che rappresentano i segmenti della timeline a TVSDK.
seo-description: I marcatori di annunci personalizzati consentono di passare una serie di specifiche TimeRange che rappresentano i segmenti della timeline a TVSDK.
seo-title: Classe TimeRange
title: Classe TimeRange
uuid: 5d0c979e-cc63-4fdd-becc-b0e3987b0891
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 0%

---


# TimeRange, classe{#timerange-class}

I marcatori di annunci personalizzati consentono di passare una serie di specifiche TimeRange che rappresentano i segmenti della timeline a TVSDK.

<!--<a id="section_42EB6D62627A424ABA250E3246EFEFC3"></a>-->

Ogni specifica `TimeRange` del set rappresenta un segmento della timeline di riproduzione mantenuto internamente da TVSDK e che deve essere correttamente contrassegnato come periodo correlato agli annunci.

La classe `TimeRange` è una semplice struttura di dati che espone la posizione iniziale e finale sulla timeline. Queste due proprietà di sola lettura riassumono l’idea di un intervallo di tempo nella timeline di riproduzione.

>[!TIP]
>
>Entrambi i valori sono espressi in millisecondi.

Di seguito è riportato un riepilogo della classe TimeRange:

```
public final class TimeRange {
    // the start/end values are provided at construction 
    public static function createRange(begin:Number, duration:Number {…}
 
    public function get begin():Number {…}
    public function get end():Number {…}
    public function get duration():Number {…}
}
```

