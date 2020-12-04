---
description: 'null'
keywords: setSecure;VideoEngineView
seo-description: 'null'
seo-title: Abilita acquisizione schermo
title: Abilita acquisizione schermo
uuid: f3d18729-e13e-47f9-b4b8-f93a2874ef16
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 0%

---


# Abilita cattura schermo{#enable-screen-capture}

TVSDK non consente l&#39;acquisizione dello schermo per impostazione predefinita. Il lettore chiama `setSecure(true)` sull&#39;oggetto `com.adobe.ave.VideoEngineView` al momento della costruzione. È possibile accedere a questo oggetto, in quanto è necessario creare un oggetto `VideoEngineView` e distribuirlo all&#39;oggetto `VideoEngine`.

Per abilitare l&#39;acquisizione dello schermo nell&#39;app:

1. Creare l&#39;oggetto `com.adobe.ave.VideoEngineView`.
1. Chiama `setSecure(false)` sull&#39;oggetto `VideoEngineView`.
