---
description: Se l'applicazione deve gestire gli eventi inviati dal gestore di funzionalità, deve registrare il gestore nel file PlayerFragment.java.
title: Gestione degli eventi
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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
