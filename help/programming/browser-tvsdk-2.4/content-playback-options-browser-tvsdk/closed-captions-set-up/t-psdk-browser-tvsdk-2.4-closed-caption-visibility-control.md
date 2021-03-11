---
description: È possibile controllare la visibilità dei sottotitoli codificati. Quando la visibilità è attiva, viene visualizzata la traccia attualmente selezionata.
title: Controllo della visibilità dei sottotitoli
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---


# Controllare la visibilità dei sottotitoli{#control-closed-caption-visibility}

È possibile controllare la visibilità dei sottotitoli codificati. Quando la visibilità è attiva, viene visualizzata la traccia attualmente selezionata.

>[!TIP]
>
>Se modifichi la traccia corrente, l’impostazione di visibilità rimane la stessa.

Se il testo della didascalia chiusa viene visualizzato quando il lettore entra nella modalità di ricerca, il testo non viene più visualizzato al termine della ricerca. Al contrario, dopo alcuni secondi, il browser TVSDK visualizza il testo della didascalia successiva nel video dopo la posizione di ricerca finale.

>[!TIP]
>
>I valori di visibilità dei sottotitoli codificati sono controllati con `MediaPlayer.VISIBLE` e `MediaPlayer.INVISIBLE`.

1. Utilizza la proprietà `MediaPlayer.ccVisibility` per accedere all’impostazione di visibilità corrente per i sottotitoli non codificati.

