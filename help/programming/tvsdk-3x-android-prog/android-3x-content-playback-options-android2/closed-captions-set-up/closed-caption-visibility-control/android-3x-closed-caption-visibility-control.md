---
description: Potete controllare la visibilità dei sottotitoli codificati. Quando la visibilità è attivata, viene visualizzato il brano attualmente selezionato. Se modificate la traccia corrente, l'impostazione di visibilità rimane invariata.
title: Controlla la visibilità dei sottotitoli
exl-id: 1fe978c5-b9ae-4e72-ac32-e3ba4e948683
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---

# Controlla la visibilità dei sottotitoli {#control-closed-caption-visibility}

Potete controllare la visibilità dei sottotitoli codificati. Quando la visibilità è attivata, viene visualizzato il brano attualmente selezionato. Se modificate la traccia corrente, l&#39;impostazione di visibilità rimane invariata.

>[!TIP]
>
>Se il testo con sottotitoli codificati viene visualizzato quando il lettore entra in modalità di ricerca, non viene più visualizzato dopo il completamento della ricerca. Invece, dopo alcuni secondi, TVSDK mostra il testo della didascalia successiva nel video dopo la posizione di ricerca finale.
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

1. Attendi `MediaPlayer` essere almeno nello stato PREPARATO. Per ulteriori informazioni, consulta [In attesa di uno stato valido](../../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/ui-configure/android-3x-ui-state-prepared-wait-for.md).

1. Per ottenere l&#39;impostazione di visibilità corrente per i sottotitoli, utilizzare il metodo getter in `MediaPlayer`, che restituisce un valore di visibilità.

   ```java
   MediaPlayer.Visibility getCCVisibility() throws MediaPlayerException;
   ```

1. Per modificare la visibilità dei sottotitoli codificati, utilizzate il metodo setter, trasmettendo un valore di visibilità da `MediaPlayer.Visibility`.

   Ad esempio:

   ```java
   mediaPlayer.setCCVisibility(MediaPlayer.Visibility visibility);
   ```
