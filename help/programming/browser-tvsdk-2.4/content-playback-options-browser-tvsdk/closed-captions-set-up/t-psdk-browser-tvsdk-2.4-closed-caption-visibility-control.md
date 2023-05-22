---
description: Potete controllare la visibilità dei sottotitoli codificati. Quando la visibilità è attiva, viene visualizzato il brano attualmente selezionato.
title: Controlla la visibilità dei sottotitoli
exl-id: e74c0344-43f3-4ed7-bbf2-d89dd3df8a33
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---

# Controlla la visibilità dei sottotitoli{#control-closed-caption-visibility}

Potete controllare la visibilità dei sottotitoli codificati. Quando la visibilità è attiva, viene visualizzato il brano attualmente selezionato.

>[!TIP]
>
>Se modificate la traccia corrente, l&#39;impostazione di visibilità rimane invariata.

Se il testo dei sottotitoli codificati viene visualizzato quando il lettore entra nella modalità di ricerca, non viene più visualizzato dopo il completamento della ricerca. Invece, dopo alcuni secondi, Browser TVSDK mostra il successivo testo della didascalia nel video dopo la posizione di ricerca finale.

>[!TIP]
>
>I valori di visibilità per i sottotitoli codificati sono controllati con `MediaPlayer.VISIBLE` e `MediaPlayer.INVISIBLE`.

1. Utilizza il `MediaPlayer.ccVisibility` per accedere all&#39;impostazione di visibilità corrente per i sottotitoli.
