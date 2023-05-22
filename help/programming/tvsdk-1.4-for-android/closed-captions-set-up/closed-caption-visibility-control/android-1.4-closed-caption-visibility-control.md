---
description: Potete controllare la visibilità dei sottotitoli codificati. Quando la visibilità è attiva, viene visualizzato il brano attualmente selezionato. Se modificate la traccia corrente, l'impostazione di visibilità rimane invariata.
title: Controlla la visibilità dei sottotitoli
exl-id: d9428744-1700-4917-b334-d6e0446eaf37
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---

# Panoramica {#control-closed-caption-visibility}

Potete controllare la visibilità dei sottotitoli codificati. Quando la visibilità è attiva, viene visualizzato il brano attualmente selezionato. Se modificate la traccia corrente, l&#39;impostazione di visibilità rimane invariata.

>[!TIP]
>
>Se il testo con sottotitoli codificati viene visualizzato quando il lettore entra nella modalità di ricerca, non viene più visualizzato dopo il completamento della ricerca. Invece, dopo alcuni secondi, TVSDK mostra il testo della didascalia successiva nel video dopo la posizione di ricerca finale.

>[!NOTE]
>
>I valori di visibilità per i sottotitoli codificati sono definiti in `MediaPlayer.Visibility`.
>
>
```java
>enum Visibility { 
>       VISIBLE,  
>       INVISIBLE 
>}
>```

1. Attendere che MediaPlayer abbia almeno lo stato READY (vedere [Attesa di uno stato valido](../../../tvsdk-1.4-for-android/ui-configure/android-1.4-ui-state-prepared-wait-for.md)).
1. Per ottenere l&#39;impostazione di visibilità corrente per i sottotitoli, utilizzare il metodo getter in MediaPlayer, che restituisce un valore di visibilità.

   ```java
   Visibility getCCVisibility() throws IllegalStateException;
   ```

1. Per modificare la visibilità dei sottotitoli codificati, utilizzate il metodo setter, trasmettendo un valore di visibilità da `MediaPlayer.Visibility`.

   Ad esempio:

   ```java
   mediaPlayer.setCCVisibility(Visibility.VISIBLE);
   ```
