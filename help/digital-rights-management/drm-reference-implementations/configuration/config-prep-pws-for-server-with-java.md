---
title: Preparare le password tramite Java
description: Preparare le password tramite Java
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '22'
ht-degree: 0%

---


# Preparare le password utilizzando Java{#prepare-passwords-using-java}

Esegui `ScrambleUtil.class` con Java:

1. Passa a `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl/scrambler/ refimpl/scrambler/`
1. Dalla riga di comando, digitare:

   ```
   java -classpath [DRM SDK DVD]/SDK/adobe-flashaccess-sdk.jar;  
       com.adobe.flashaccess.refimpl.util.ScrambleUtil your_pfx_password
   ```

