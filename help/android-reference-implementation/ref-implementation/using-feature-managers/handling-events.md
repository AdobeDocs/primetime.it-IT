---
description: Se l'applicazione deve gestire gli eventi inviati dal gestore di funzionalità, deve registrare il gestore nel file PlayerFragment.java.
title: Gestione degli eventi
exl-id: 4c9a76bb-071e-4408-819c-a7611fe615cd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '50'
ht-degree: 0%

---

# Gestione degli eventi {#handling-events}

Se l&#39;applicazione deve gestire gli eventi inviati dal gestore di funzionalità, deve registrare il gestore nel file PlayerFragment.java.

Ad esempio:

```
private final AdsManager.AdsManagerEventListener adsManagerEventListener =  
  new AdsManager.AdsManagerEventListener() { 
 
    // add the ads functionality... 
 
} 
 
//Register the listener 
adsManager.addEventListener(adsManagerEventListener);
```
