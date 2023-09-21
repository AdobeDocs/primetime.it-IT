---
title: Preparare le password utilizzando Ant
description: Preparare le password utilizzando Ant
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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
