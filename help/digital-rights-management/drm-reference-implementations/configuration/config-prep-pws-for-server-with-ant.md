---
description: 'null'
seo-description: 'null'
seo-title: Preparare le password utilizzando Ant
title: Preparare le password utilizzando Ant
uuid: 9419ab0d-b448-4881-9d26-35c00f0b13bc
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Preparare le password utilizzando Ant{#prepare-passwords-using-ant}

Usa Ant per crittografare la password:

1. Passa a `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl/`
1. Impostate la `sdkdir` proprietà in [!DNL build-refimpl.xml] modo che punti alla directory che include Primetime DRM Java SDK.
1. Eseguite il comando seguente:

   ```
   ant -f build-refimpl.xml
   ```

