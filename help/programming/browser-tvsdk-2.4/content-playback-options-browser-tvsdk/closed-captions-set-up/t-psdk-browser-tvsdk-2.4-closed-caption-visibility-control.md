---
description: È possibile controllare la visibilità dei sottotitoli codificati. Quando la visibilità è attivata, viene visualizzata la traccia attualmente selezionata.
seo-description: È possibile controllare la visibilità dei sottotitoli codificati. Quando la visibilità è attivata, viene visualizzata la traccia attualmente selezionata.
seo-title: Controllo della visibilità dei sottotitoli
title: Controllo della visibilità dei sottotitoli
uuid: b161a729-73f3-4019-a95e-013b42779842
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---


# Controllare la visibilità dei sottotitoli codificati{#control-closed-caption-visibility}

È possibile controllare la visibilità dei sottotitoli codificati. Quando la visibilità è attivata, viene visualizzata la traccia attualmente selezionata.

>[!TIP]
>
>Se modificate la traccia corrente, l’impostazione di visibilità rimane la stessa.

Se il testo della didascalia chiusa viene visualizzato quando il lettore entra nella modalità di ricerca, il testo non viene più visualizzato al termine della ricerca. Al contrario, dopo alcuni secondi, Browser TVSDK visualizza il testo della didascalia successiva nel video dopo la posizione di ricerca finale.

>[!TIP]
>
>I valori di visibilità per i sottotitoli codificati sono controllati da `MediaPlayer.VISIBLE` e `MediaPlayer.INVISIBLE`.

1. Utilizzare la proprietà `MediaPlayer.ccVisibility` per accedere all&#39;impostazione di visibilità corrente per i sottotitoli codificati.

