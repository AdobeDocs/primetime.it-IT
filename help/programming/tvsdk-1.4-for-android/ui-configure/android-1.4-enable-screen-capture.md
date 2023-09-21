---
keywords: setSecure;VideoEngineView
title: Abilita acquisizione schermo
description: Abilita acquisizione schermo
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 0%

---

# Abilita acquisizione schermo{#enable-screen-capture}

Per impostazione predefinita, TVSDK non consente l’acquisizione dello schermo. Il lettore chiama `setSecure(true)` il `com.adobe.ave.VideoEngineView` oggetto al momento della costruzione. Si dispone dell&#39;accesso a questo oggetto, poiché è necessario creare un `VideoEngineView` e fornirlo al `VideoEngine` oggetto.

Per abilitare l’acquisizione schermata nell’app:

1. Creare `com.adobe.ave.VideoEngineView` oggetto.
1. Chiamata `setSecure(false)` sul tuo `VideoEngineView` oggetto.
