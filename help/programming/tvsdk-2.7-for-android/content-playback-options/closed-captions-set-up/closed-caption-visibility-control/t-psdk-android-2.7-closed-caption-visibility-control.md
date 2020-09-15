---
description: È possibile controllare la visibilità dei sottotitoli codificati. Quando la visibilità è attivata, viene visualizzata la traccia attualmente selezionata. Se modificate la traccia corrente, l’impostazione di visibilità rimane la stessa.
seo-description: È possibile controllare la visibilità dei sottotitoli codificati. Quando la visibilità è attivata, viene visualizzata la traccia attualmente selezionata. Se modificate la traccia corrente, l’impostazione di visibilità rimane la stessa.
seo-title: Controllo della visibilità dei sottotitoli
title: Controllo della visibilità dei sottotitoli
uuid: b9d48d70-2554-4948-8654-fa45093c3782
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# Panoramica {#control-closed-caption-visibility-overview}

È possibile controllare la visibilità dei sottotitoli codificati. Quando la visibilità è attivata, viene visualizzata la traccia attualmente selezionata. Se modificate la traccia corrente, l’impostazione di visibilità rimane la stessa.

>[!TIP]
>
>Se il testo della didascalia chiusa viene visualizzato quando il lettore attiva la modalità di ricerca, il testo non viene più visualizzato al termine della ricerca. Al contrario, dopo alcuni secondi, TVSDK visualizza il testo della didascalia successiva nel video dopo la posizione di ricerca finale.
>
>I valori di visibilità per le didascalie chiuse sono definiti in `MediaPlayer.Visibility`.
>
>
```java
>enum Visibility {  
>       VISIBLE,  
>       INVISIBLE 
>}
>```

1. Attendete che lo stato `MediaPlayer` sia almeno PREPARATO.

   Per ulteriori informazioni, consulta Pronto-attesa-stato-ui.
1. Per ottenere l’impostazione di visibilità corrente per i sottotitoli codificati, utilizzate il metodo getter in `MediaPlayer`, che restituisce un valore di visibilità.

   ```java
   MediaPlayer.Visibility getCCVisibility() throws MediaPlayerException;
   ```

1. Per modificare la visibilità dei sottotitoli codificati, utilizzate il metodo setter, passando un valore di visibilità da `MediaPlayer.Visibility`.

   Ad esempio:

   ```java
   mediaPlayer.setCCVisibility(MediaPlayer.Visibility visibility);
   ```

