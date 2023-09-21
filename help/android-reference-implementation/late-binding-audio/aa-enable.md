---
description: È possibile integrare nel lettore flussi audio alternativi o di associazione tardiva creando un gestore di funzioni audio alternativo.
title: Integrare l’audio di associazione tardiva
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 0%

---

# Integrare l’audio di associazione tardiva {#integrate-late-binding-audio}

È possibile integrare nel lettore flussi audio alternativi o di associazione tardiva creando un gestore di funzioni audio alternativo.

* Per creare un gestore audio alternativo:

  ```java
  AAManager aaManager = new AAManagerOn(); 
  ```

* Per utilizzare ManagerFactory per abilitare l&#39;audio alternativo, assicurarsi che la seguente riga di codice sia nel `PlayerFragment.java` file:

  ```java
  aaManager = ManagerFactory.getAAManager( 
  <b>true</b>,config, mediaPlayer);
  ```

  Per disattivare l&#39;audio alternativo:

  ```java
  aaManager = ManagerFactory.getAAManager( 
  <b>false</b>,config, mediaPlayer);
  ```
