---
description: È possibile controllare la visibilità dei sottotitoli codificati. Quando la visibilità è abilitata, viene visualizzata la traccia attualmente selezionata. Se modifichi la traccia corrente, l’impostazione di visibilità rimane la stessa.
title: Controllo della visibilità dei sottotitoli
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 1%

---


# Panoramica {#control-closed-caption-visibility-overview}

È possibile controllare la visibilità dei sottotitoli codificati. Quando la visibilità è abilitata, viene visualizzata la traccia attualmente selezionata. Se modifichi la traccia corrente, l’impostazione di visibilità rimane la stessa.

>[!TIP]
>
>Se il testo della didascalia chiusa viene visualizzato quando il lettore entra in modalità di ricerca, il testo non viene più visualizzato al termine della ricerca. Al contrario, dopo alcuni secondi, TVSDK visualizza il testo della didascalia successiva nel video dopo la posizione di ricerca finale.
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

1. Attendi che lo stato `MediaPlayer` sia almeno PREPARATO.

   Per ulteriori informazioni, consulta ui-state-ready-wait-for .
1. Per ottenere l’impostazione di visibilità corrente per i sottotitoli codificati, utilizza il metodo getter in `MediaPlayer`, che restituisce un valore di visibilità.

   ```java
   MediaPlayer.Visibility getCCVisibility() throws MediaPlayerException;
   ```

1. Per modificare la visibilità dei sottotitoli codificati, utilizzare il metodo setter, passando un valore di visibilità da `MediaPlayer.Visibility`.

   Ad esempio:

   ```java
   mediaPlayer.setCCVisibility(MediaPlayer.Visibility visibility);
   ```

