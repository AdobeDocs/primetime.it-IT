---
title: Riproduzione automatica in iOS
description: Riproduzione automatica in iOS
copied-description: true
exl-id: 591e8f74-63c3-4f74-9df4-024eb8aab646
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '93'
ht-degree: 0%

---

# Riproduzione automatica in iOS{#autoplay-on-ios}

L’implementazione dell’API del volume di AdobePSDK.MediaPlayer consente la riproduzione automatica dei contenuti sui dispositivi che eseguono iOS versione 10 o successiva. iOS consente la riproduzione automatica solo quando il volume è disattivato. Quando il volume è impostato su zero, l’API imposta il `muted` proprietà del tag video a `true`, altrimenti il `muted` proprietà impostata su `false`. Il `play` L’API avvia la riproduzione senza alcuna interazione da parte dell’utente o gesto da parte dell’utente.

Per la riproduzione automatica su iPhone, imposta inoltre `playsInline` proprietà del `video` tag a `true`.

```
videoDiv.getElementsByTagName('video')[0].playsInline = true;
```

>[!NOTE]
>
>Uso di `playsInline` avvia la riproduzione senza la modalità a schermo intero.
