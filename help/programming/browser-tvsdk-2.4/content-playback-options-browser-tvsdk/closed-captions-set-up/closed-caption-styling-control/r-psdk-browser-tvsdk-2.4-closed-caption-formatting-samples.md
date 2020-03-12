---
description: È possibile specificare la formattazione dei sottotitoli codificati.
seo-description: È possibile specificare la formattazione dei sottotitoli codificati.
seo-title: Esempi di formattazione delle didascalie
title: Esempi di formattazione delle didascalie
uuid: d55a506a-6662-4252-95f6-4073b2997f3b
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Esempi: Formattazione delle didascalie{#examples-caption-formatting}

È possibile specificare la formattazione dei sottotitoli codificati.

## Esempio 1: Specificare in modo esplicito i valori di formato {#section_BD7B48F3B66D4E9290E1CB2F464E08E4}

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
>Il browser TVSDK non supporta l&#39;opacità del bordo del font, del colore di riempimento o del riempimento.

