---
description: I marcatori di annunci personalizzati ti consentono di trasmettere a TVSDK un set di specifiche TimeRange che rappresentano i segmenti della timeline.
title: TimeRange, classe
exl-id: f86dee89-15de-4caa-b05c-3e08516b32ce
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---

# TimeRange, classe {#timerange-class}

I marcatori di annunci personalizzati ti consentono di trasmettere a TVSDK un set di specifiche TimeRange che rappresentano i segmenti della timeline.

<!--<a id="section_42EB6D62627A424ABA250E3246EFEFC3"></a>-->

Ogni `TimeRange` La specifica nel set rappresenta un segmento nella timeline di riproduzione gestito internamente da TVSDK e che deve essere contrassegnato in modo appropriato come periodo relativo agli annunci.

Il `TimeRange` La classe è una semplice struttura di dati che espone la posizione iniziale e finale sulla timeline. Queste due proprietà di sola lettura astraggono l’idea di un intervallo di tempo nella timeline di riproduzione.

>[!TIP]
>
>Entrambi i valori sono espressi in millisecondi.

Riepilogo del `TimeRange` classe:

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
