---
description: Se l'applicazione deve gestire gli eventi inviati dal gestore di funzioni, deve registrare il manager nel file PlayerFragment.java .
title: Gestione degli eventi
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '50'
ht-degree: 4%

---


# Gestione degli eventi {#handling-events}

Se l&#39;applicazione deve gestire gli eventi inviati dal gestore di funzioni, deve registrare il manager nel file PlayerFragment.java .

Ad esempio:

```
private final AdsManager.AdsManagerEventListener adsManagerEventListener =  
  new AdsManager.AdsManagerEventListener() { 
 
    // add the ads functionality... 
 
} 
 
//Register the listener 
adsManager.addEventListener(adsManagerEventListener);
```
