---
description: 'null'
seo-description: 'null'
seo-title: Esecuzione automatica su iOS
title: Esecuzione automatica su iOS
uuid: d15bad24-be50-49e5-90f4-68dbda96fb6d
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Esecuzione automatica su iOS{#autoplay-on-ios}

L&#39;implementazione dell&#39;API volume di AdobePSDK.MediaPlayer consente la riproduzione automatica del contenuto sui dispositivi con iOS versione 10 o successiva. iOS consente la riproduzione automatica solo quando il volume è disattivato. Quando il volume è impostato su zero, l&#39;API imposta la `muted` proprietà del tag video su `true`, altrimenti la `muted` proprietà viene impostata su `false`. L&#39; `play` API avvia la riproduzione senza alcuna interazione con l&#39;utente o senza alcun gesto da parte dell&#39;utente.

Per la riproduzione automatica su iPhone, impostate anche la `playsInline` proprietà del `video` tag su `true`.

```
videoDiv.getElementsByTagName('video')[0].playsInline = true;
```

>[!NOTE]
>
>L&#39;utilizzo di `playsInline` proprietà avvia la riproduzione senza la modalità a schermo intero.

