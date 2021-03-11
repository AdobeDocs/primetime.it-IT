---
description: È possibile integrare flussi audio in ritardo o alternati nel lettore creando un gestore di funzioni audio alternativo.
title: Integrare l’audio in ritardo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 0%

---


# Integrare l&#39;audio in ritardo {#integrate-late-binding-audio}

È possibile integrare flussi audio in ritardo o alternati nel lettore creando un gestore di funzioni audio alternativo.

* Per creare una gestione audio alternativa:

   ```java
   AAManager aaManager = new AAManagerOn(); 
   ```

* Per utilizzare ManagerFactory per abilitare l&#39;audio alternativo, assicurati che la seguente riga di codice sia nel file `PlayerFragment.java`:

   ```java
   aaManager = ManagerFactory.getAAManager( 
   <b>true</b>,config, mediaPlayer);
   ```

   Per disabilitare l&#39;audio alternativo:

   ```java
   aaManager = ManagerFactory.getAAManager( 
   <b>false</b>,config, mediaPlayer);
   ```

