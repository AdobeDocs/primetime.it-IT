---
description: È possibile integrare flussi audio alterni o in associazione tardiva nel lettore creando un gestore di funzioni audio alternativo.
seo-description: È possibile integrare flussi audio alterni o in associazione tardiva nel lettore creando un gestore di funzioni audio alternativo.
seo-title: Integrare l'audio con binding ritardato
title: Integrare l'audio con binding ritardato
uuid: cd2e259a-2af4-4d7b-a856-79bd087e8ca6
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# Integrare l&#39;audio con binding ritardato {#integrate-late-binding-audio}

È possibile integrare flussi audio alterni o in associazione tardiva nel lettore creando un gestore di funzioni audio alternativo.

* Per creare una gestione audio alternativa:

   ```java
   AAManager aaManager = new AAManagerOn(); 
   ```

* Per utilizzare ManagerFactory per abilitare l&#39;audio alternativo, accertatevi che nel `PlayerFragment.java` file sia presente la seguente riga di codice:

   ```java
   aaManager = ManagerFactory.getAAManager( 
   <b>true</b>,config, mediaPlayer);
   ```

   Per disattivare l&#39;audio alternativo:

   ```java
   aaManager = ManagerFactory.getAAManager( 
   <b>false</b>,config, mediaPlayer);
   ```

