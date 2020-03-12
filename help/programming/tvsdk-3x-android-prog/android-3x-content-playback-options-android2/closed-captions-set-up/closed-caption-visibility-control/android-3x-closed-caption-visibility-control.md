---
description: È possibile controllare la visibilità dei sottotitoli codificati. Quando la visibilità è attivata, viene visualizzata la traccia attualmente selezionata. Se modificate la traccia corrente, l’impostazione di visibilità rimane la stessa.
seo-description: È possibile controllare la visibilità dei sottotitoli codificati. Quando la visibilità è attivata, viene visualizzata la traccia attualmente selezionata. Se modificate la traccia corrente, l’impostazione di visibilità rimane la stessa.
seo-title: Controllo della visibilità dei sottotitoli
title: Controllo della visibilità dei sottotitoli
uuid: f142e60d-5581-4d1c-9d4d-a4a58ac1b67b
translation-type: tm+mt
source-git-commit: ed910a60440ae7c0d19d9be56c80c8bdbc62bcf1

---


# Controllo della visibilità dei sottotitoli {#control-closed-caption-visibility}

È possibile controllare la visibilità dei sottotitoli codificati. Quando la visibilità è attivata, viene visualizzata la traccia attualmente selezionata. Se modificate la traccia corrente, l’impostazione di visibilità rimane la stessa.

>[!TIP]
>
>Se il testo della didascalia chiusa viene visualizzato quando il lettore attiva la modalità di ricerca, il testo non viene più visualizzato al termine della ricerca. Al contrario, dopo alcuni secondi, TVSDK visualizza il testo della didascalia successiva nel video dopo la posizione di ricerca finale.
>
>I valori di visibilità per le didascalie chiuse sono definiti in `MediaPlayer.Visibility`. >
>
```java>
>enum Visibility {  
>       VISIBLE,  
>       INVISIBLE 
>}
>```>



1. Attendete che lo stato `MediaPlayer` sia almeno PREPARATO. Per ulteriori informazioni, vedere [Aspettare uno stato](../../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/ui-configure/android-3x-ui-state-prepared-wait-for.md)valido.

1. Per ottenere l’impostazione di visibilità corrente per i sottotitoli codificati, utilizzate il metodo getter in `MediaPlayer`, che restituisce un valore di visibilità.

   ```java
   MediaPlayer.Visibility getCCVisibility() throws MediaPlayerException;
   ```

1. Per modificare la visibilità dei sottotitoli codificati, utilizzate il metodo setter, passando un valore di visibilità da `MediaPlayer.Visibility`.

   Ad esempio:

   ```java
   mediaPlayer.setCCVisibility(MediaPlayer.Visibility visibility);
   ```
