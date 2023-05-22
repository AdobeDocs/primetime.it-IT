---
description: È possibile integrare nel lettore flussi audio alternativi o di associazione tardiva creando un gestore di funzioni audio alternativo.
title: Integrare l’audio di associazione tardiva
exl-id: 43be9042-d547-4646-a920-cdd2a5dbb1fb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
