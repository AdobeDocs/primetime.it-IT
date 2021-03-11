---
title: Preparare le password con Ant
description: Preparare le password con Ant
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '40'
ht-degree: 0%

---


# Prepara le password con Ant{#prepare-passwords-using-ant}

Usa Ant per crittografare la password:

1. Passa a `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl/`
1. Imposta la proprietà `sdkdir` in [!DNL build-refimpl.xml] per puntare alla directory che include l&#39;SDK Java DRM di Primetime.
1. Esegui il comando seguente:

   ```
   ant -f build-refimpl.xml
   ```

