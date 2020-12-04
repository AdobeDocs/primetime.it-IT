---
description: Se l'applicazione deve gestire gli eventi inviati dal gestore di funzioni, deve registrare il manager nel file PlayerFragment.java.
seo-description: Se l'applicazione deve gestire gli eventi inviati dal gestore di funzioni, deve registrare il manager nel file PlayerFragment.java.
seo-title: Gestione degli eventi
title: Gestione degli eventi
uuid: 13639f02-0dcc-4a0a-8524-515da5478006
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '74'
ht-degree: 2%

---


# Gestione degli eventi {#handling-events}

Se l&#39;applicazione deve gestire gli eventi inviati dal gestore di funzioni, deve registrare il manager nel file PlayerFragment.java.

Ad esempio:

```
private final AdsManager.AdsManagerEventListener adsManagerEventListener =  
  new AdsManager.AdsManagerEventListener() { 
 
    // add the ads functionality... 
 
} 
 
//Register the listener 
adsManager.addEventListener(adsManagerEventListener);
```
