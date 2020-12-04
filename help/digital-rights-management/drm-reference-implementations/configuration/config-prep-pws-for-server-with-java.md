---
description: 'null'
seo-description: 'null'
seo-title: Preparare le password tramite Java
title: Preparare le password tramite Java
uuid: 8a708d22-764f-4229-95ca-109482563432
translation-type: tm+mt
source-git-commit: 055989cbe3a187516f18816492aaea709cc80c81
workflow-type: tm+mt
source-wordcount: '24'
ht-degree: 0%

---


# Preparare le password utilizzando Java{#prepare-passwords-using-java}

Eseguire `ScrambleUtil.class` con Java:

1. Passa a `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl/scrambler/ refimpl/scrambler/`
1. Dalla riga di comando, digitare:

   ```
   java -classpath [DRM SDK DVD]/SDK/adobe-flashaccess-sdk.jar;  
       com.adobe.flashaccess.refimpl.util.ScrambleUtil your_pfx_password
   ```

