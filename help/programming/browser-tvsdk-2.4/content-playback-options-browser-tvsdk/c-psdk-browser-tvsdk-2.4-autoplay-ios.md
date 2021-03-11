---
title: Riproduzione automatica su iOS
description: Riproduzione automatica su iOS
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '93'
ht-degree: 0%

---


# Riproduzione automatica su iOS{#autoplay-on-ios}

L&#39;implementazione dell&#39;API del volume di AdobePSDK.MediaPlayer consente la riproduzione automatica dei contenuti sui dispositivi con iOS versione 10 o superiore. iOS consente la riproduzione automatica solo quando il volume è disattivato. Quando il volume è impostato su zero, l&#39;API imposta la proprietà `muted` del tag video su `true`, altrimenti la proprietà `muted` viene impostata su `false`. L&#39;API `play` avvia la riproduzione senza alcuna interazione da parte dell&#39;utente o alcun gesto dell&#39;utente.

Per la riproduzione automatica su iPhone, imposta anche la proprietà `playsInline` del tag `video` su `true`.

```
videoDiv.getElementsByTagName('video')[0].playsInline = true;
```

>[!NOTE]
>
>L&#39;utilizzo della proprietà `playsInline` avvia la riproduzione senza la modalità a schermo intero.

