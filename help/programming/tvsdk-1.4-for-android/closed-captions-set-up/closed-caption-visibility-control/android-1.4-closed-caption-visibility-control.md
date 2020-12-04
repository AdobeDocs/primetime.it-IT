---
description: È possibile controllare la visibilità dei sottotitoli codificati. Quando la visibilità è attivata, viene visualizzata la traccia attualmente selezionata. Se modificate la traccia corrente, l’impostazione di visibilità rimane la stessa.
seo-description: È possibile controllare la visibilità dei sottotitoli codificati. Quando la visibilità è attivata, viene visualizzata la traccia attualmente selezionata. Se modificate la traccia corrente, l’impostazione di visibilità rimane la stessa.
seo-title: Controllo della visibilità dei sottotitoli
title: Controllo della visibilità dei sottotitoli
uuid: 42913347-8158-474e-aa3c-ba4d38baba12
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# Panoramica {#control-closed-caption-visibility}

È possibile controllare la visibilità dei sottotitoli codificati. Quando la visibilità è attivata, viene visualizzata la traccia attualmente selezionata. Se modificate la traccia corrente, l’impostazione di visibilità rimane la stessa.

>[!TIP]
>
>Se il testo della didascalia chiusa viene visualizzato quando il lettore entra nella modalità di ricerca, il testo non viene più visualizzato al termine della ricerca. Al contrario, dopo alcuni secondi, TVSDK visualizza il testo della didascalia successiva nel video dopo la posizione di ricerca finale.

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

1. Attendete che MediaPlayer disponga almeno dello stato PREPARATO (vedere [Attendere uno stato valido](../../../tvsdk-1.4-for-android/ui-configure/android-1.4-ui-state-prepared-wait-for.md)).
1. Per ottenere l’impostazione di visibilità corrente per i sottotitoli codificati, utilizzate il metodo getter in MediaPlayer, che restituisce un valore di visibilità.

   ```java
   Visibility getCCVisibility() throws IllegalStateException;
   ```

1. Per modificare la visibilità dei sottotitoli codificati, utilizzate il metodo setter, passando un valore di visibilità da `MediaPlayer.Visibility`.

   Ad esempio:

   ```java
   mediaPlayer.setCCVisibility(Visibility.VISIBLE);
   ```

