---
title: Preparare le password utilizzando Ant
description: Preparare le password utilizzando Ant
copied-description: true
exl-id: 78f00fd7-ca9c-49a9-9e4b-6d1e2daf9241
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '40'
ht-degree: 0%

---

# Preparare le password utilizzando Ant{#prepare-passwords-using-ant}

Utilizza Ant per crittografare la password:

1. Accedi a `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl/`
1. Imposta il `sdkdir` proprietà in [!DNL build-refimpl.xml] per puntare alla directory che include Primetime DRM Java SDK.
1. Esegui il comando seguente:

   ```
   ant -f build-refimpl.xml
   ```
