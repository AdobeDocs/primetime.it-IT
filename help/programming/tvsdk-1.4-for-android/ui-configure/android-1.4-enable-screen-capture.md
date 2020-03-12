---
description: 'null'
keywords: setSecure;VideoEngineView
seo-description: 'null'
seo-title: Abilita acquisizione schermo
title: Abilita acquisizione schermo
uuid: f3d18729-e13e-47f9-b4b8-f93a2874ef16
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Abilita acquisizione schermo{#enable-screen-capture}

TVSDK non consente l&#39;acquisizione dello schermo per impostazione predefinita. Il giocatore chiama `setSecure(true)` l&#39; `com.adobe.ave.VideoEngineView` oggetto in fase di costruzione. È possibile accedere a questo oggetto, in quanto è necessario creare un `VideoEngineView` oggetto e fornirlo all&#39; `VideoEngine` oggetto.

Per abilitare l&#39;acquisizione dello schermo nell&#39;app:

1. Creare l&#39; `com.adobe.ave.VideoEngineView` oggetto.
1. Chiama `setSecure(false)` il tuo `VideoEngineView` oggetto.
