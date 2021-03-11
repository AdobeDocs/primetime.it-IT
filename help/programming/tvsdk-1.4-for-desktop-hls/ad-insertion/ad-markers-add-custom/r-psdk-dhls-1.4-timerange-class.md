---
description: I marcatori di annunci personalizzati ti consentono di trasmettere a TVSDK un set di specifiche TimeRange che rappresentano i segmenti della timeline.
title: Classe TimeRange
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---


# Classe TimeRange{#timerange-class}

I marcatori di annunci personalizzati ti consentono di trasmettere a TVSDK un set di specifiche TimeRange che rappresentano i segmenti della timeline.

<!--<a id="section_42EB6D62627A424ABA250E3246EFEFC3"></a>-->

Ogni specifica `TimeRange` del set rappresenta un segmento nella timeline di riproduzione mantenuto internamente da TVSDK e che deve essere contrassegnato in modo appropriato come periodo correlato all’annuncio.

La classe `TimeRange` è una semplice struttura di dati che espone la posizione iniziale e finale sulla timeline. Queste due proprietà di sola lettura astraggono l&#39;idea di un intervallo di tempo nella timeline di riproduzione.

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

