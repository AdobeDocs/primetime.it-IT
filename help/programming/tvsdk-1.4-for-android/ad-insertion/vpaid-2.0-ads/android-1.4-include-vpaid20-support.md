---
description: Per aggiungere il supporto VPAID 2.0, aggiungi una visualizzazione annunci personalizzata e gli ascoltatori appropriati.
title: Implementare l’integrazione con VPAID 2.0
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '50'
ht-degree: 0%

---


# Implementare l&#39;integrazione VPAID 2.0{#implement-vpaid-integration}

Per aggiungere il supporto VPAID 2.0, aggiungi una visualizzazione annunci personalizzata e gli ascoltatori appropriati.

Per aggiungere il supporto VPAID 2.0:

1. Aggiungi la visualizzazione annunci personalizzata all’interfaccia del lettore.

   ```java
   _playerFrame.addView(mediaPlayer.createCustomAdView());
   ```

1. Aggiungi un listener per gli eventi di annunci personalizzati.

   ```java
   mediaplayer.addEventListener(MediaPlayer.Event.CUSTOM_AD,  
     _customAdEventListener);
   ```

