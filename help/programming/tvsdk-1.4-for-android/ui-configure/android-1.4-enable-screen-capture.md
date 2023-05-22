---
keywords: setSecure;VideoEngineView
title: Abilita acquisizione schermo
description: Abilita acquisizione schermo
copied-description: true
exl-id: 5dd1bf4e-ab50-4b57-89e4-eacc291a9fe3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 0%

---

# Abilita acquisizione schermo{#enable-screen-capture}

Per impostazione predefinita, TVSDK non consente l’acquisizione dello schermo. Il lettore chiama `setSecure(true)` il `com.adobe.ave.VideoEngineView` oggetto al momento della costruzione. Si dispone dell&#39;accesso a questo oggetto, poiché è necessario creare un `VideoEngineView` e fornirlo al `VideoEngine` oggetto.

Per abilitare l’acquisizione schermata nell’app:

1. Creare `com.adobe.ave.VideoEngineView` oggetto.
1. Chiamata `setSecure(false)` sul tuo `VideoEngineView` oggetto.
