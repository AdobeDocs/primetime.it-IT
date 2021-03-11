---
description: È possibile controllare la visibilità dei sottotitoli codificati. Quando la visibilità è attiva, viene visualizzata la traccia attualmente selezionata. Se modifichi la traccia corrente, l’impostazione di visibilità rimane la stessa.
title: Controllo della visibilità dei sottotitoli
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 1%

---


# Panoramica {#control-closed-caption-visibility}

È possibile controllare la visibilità dei sottotitoli codificati. Quando la visibilità è attiva, viene visualizzata la traccia attualmente selezionata. Se modifichi la traccia corrente, l’impostazione di visibilità rimane la stessa.

>[!TIP]
>
>Se il testo della didascalia chiusa viene visualizzato quando il lettore entra nella modalità di ricerca, il testo non viene più visualizzato al termine della ricerca. Al contrario, dopo alcuni secondi, TVSDK visualizza il testo della didascalia successiva nel video dopo la posizione di ricerca finale.

>[!NOTE]
>
>I valori di visibilità dei sottotitoli codificati sono definiti in `MediaPlayer.Visibility`.
>
>
```java
>enum Visibility { 
>       VISIBLE,  
>       INVISIBLE 
>}
>```

1. Attendi che MediaPlayer disponga almeno dello stato PREPARATO (vedi [Attendi uno stato valido](../../../tvsdk-1.4-for-android/ui-configure/android-1.4-ui-state-prepared-wait-for.md)).
1. Per ottenere l&#39;impostazione di visibilità corrente per i sottotitoli codificati, utilizza il metodo getter in MediaPlayer, che restituisce un valore di visibilità.

   ```java
   Visibility getCCVisibility() throws IllegalStateException;
   ```

1. Per modificare la visibilità dei sottotitoli codificati, utilizzare il metodo setter, passando un valore di visibilità da `MediaPlayer.Visibility`.

   Ad esempio:

   ```java
   mediaPlayer.setCCVisibility(Visibility.VISIBLE);
   ```

