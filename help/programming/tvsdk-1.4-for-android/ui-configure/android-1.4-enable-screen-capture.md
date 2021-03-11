---
keywords: setSecure;VideoEngineView
title: Abilita l’acquisizione dello schermo
description: Abilita l’acquisizione dello schermo
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 0%

---


# Abilita l&#39;acquisizione dello schermo{#enable-screen-capture}

TVSDK disabilita l’acquisizione dello schermo per impostazione predefinita. Il lettore chiama `setSecure(true)` sull&#39;oggetto `com.adobe.ave.VideoEngineView` in fase di costruzione. È possibile accedere a questo oggetto, in quanto è necessario creare un oggetto `VideoEngineView` e fornirlo all&#39;oggetto `VideoEngine`.

Per abilitare l’acquisizione da schermo nell’app:

1. Crea l&#39;oggetto `com.adobe.ave.VideoEngineView` .
1. Chiama `setSecure(false)` sull&#39;oggetto `VideoEngineView`.
