---
description: È possibile specificare la formattazione dei sottotitoli.
title: Esempi di formattazione dei sottotitoli
exl-id: 946530a1-c7d7-4582-81b8-71b2980561cb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '33'
ht-degree: 0%

---

# Esempi: Formattazione dei sottotitoli{#examples-caption-formatting}

È possibile specificare la formattazione dei sottotitoli.

## Esempio 1: specificare esplicitamente i valori di formato {#section_BD7B48F3B66D4E9290E1CB2F464E08E4}

```js
// Set CC style. 
var tf = new AdobePSDK.TextFormat( 
      AdobePSDK.TextFormat.FONT_DEFAULT, 
      AdobePSDK.TextFormat.COLOR_DEFAULT, 
      AdobePSDK.TextFormat.COLOR_DEFAULT, 
      AdobePSDK.TextFormat.FONT_EDGE_DEFAULT, 
      AdobePSDK.TextFormat.COLOR_DEFAULT, 
      AdobePSDK.TextFormat.COLOR_DEFAULT, 
      AdobePSDK.TextFormat.SIZE_DEFAULT, 
      AdobePSDK.TextFormat.DEFAULT_OPACITY, 
      AdobePSDK.TextFormat.DEFAULT_OPACITY, 
      AdobePSDK.TextFormat.DEFAULT_OPACITY; 
 mediaPlayer.CCStyle(tf);
```

>[!IMPORTANT]
>
>Il TVSDK del browser non supporta il bordo del font, il colore di riempimento o l’opacità del riempimento.
