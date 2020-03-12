---
description: I marcatori di annunci personalizzati consentono di passare una serie di specifiche TimeRange che rappresentano i segmenti della timeline a TVSDK.
seo-description: I marcatori di annunci personalizzati consentono di passare una serie di specifiche TimeRange che rappresentano i segmenti della timeline a TVSDK.
seo-title: Classe TimeRange
title: Classe TimeRange
uuid: e5a176af-29b9-4aa6-848e-5aba7988584b
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Classe TimeRange {#timerange-class}

I marcatori di annunci personalizzati consentono di passare una serie di specifiche TimeRange che rappresentano i segmenti della timeline a TVSDK.

<!--<a id="section_42EB6D62627A424ABA250E3246EFEFC3"></a>-->

Ogni `TimeRange` specifica del set rappresenta un segmento nella timeline di riproduzione che viene mantenuto internamente da TVSDK e deve essere correttamente contrassegnato come periodo correlato agli annunci.

La `TimeRange` classe è una semplice struttura di dati che espone la posizione iniziale e finale sulla timeline. Queste due proprietà di sola lettura riassumono l’idea di un intervallo di tempo nella timeline di riproduzione.

>[!TIP]
>
>Entrambi i valori sono espressi in millisecondi.

Di seguito è riportato un riepilogo della `TimeRange` classe:

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

