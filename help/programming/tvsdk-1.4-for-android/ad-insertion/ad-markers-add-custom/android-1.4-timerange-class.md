---
description: I marcatori di annunci personalizzati consentono di passare una serie di specifiche TimeRange che rappresentano i segmenti della timeline a TVSDK.
seo-description: I marcatori di annunci personalizzati consentono di passare una serie di specifiche TimeRange che rappresentano i segmenti della timeline a TVSDK.
seo-title: Classe TimeRange
title: Classe TimeRange
uuid: adf4f1ad-6b3b-48ac-a388-ee1fd54f770b
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 0%

---


# TimeRange, classe{#timerange-class}

I marcatori di annunci personalizzati consentono di passare una serie di specifiche TimeRange che rappresentano i segmenti della timeline a TVSDK.

<!--<a id="section_42EB6D62627A424ABA250E3246EFEFC3"></a>-->

Ogni specifica TimeRange nel set rappresenta un segmento nella timeline di riproduzione mantenuto internamente da TVSDK e che deve essere correttamente contrassegnato come periodo correlato agli annunci.

La classe `TimeRange` è una semplice struttura di dati che espone la posizione iniziale e finale sulla timeline. Queste due proprietà di sola lettura riassumono l’idea di un intervallo di tempo nella timeline di riproduzione.

>[!TIP]
>
>Entrambi i valori sono espressi in millisecondi.

Di seguito è riportato un riepilogo della classe `TimeRange`:

```java
public final class TimeRange {
    // the start/end values are provided at construction time
    public static TimeRange createRange(long begin, long duration) {...} 

    // only getters are available
    public long getBegin() {...} 
    public long getEnd() {...} 
    public long getDuration() {...}
}
```

