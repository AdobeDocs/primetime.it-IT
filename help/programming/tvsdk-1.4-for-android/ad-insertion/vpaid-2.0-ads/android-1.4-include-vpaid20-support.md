---
description: Per aggiungere il supporto VPAID 2.0, aggiungi una visualizzazione ad personalizzata e i listener appropriati.
seo-description: Per aggiungere il supporto VPAID 2.0, aggiungi una visualizzazione ad personalizzata e i listener appropriati.
seo-title: Implementare l'integrazione VPAID 2.0
title: Implementare l'integrazione VPAID 2.0
uuid: 7d11ffd8-240c-4a95-94e6-ff4417c8942e
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Implementare l&#39;integrazione VPAID 2.0{#implement-vpaid-integration}

Per aggiungere il supporto VPAID 2.0, aggiungi una visualizzazione ad personalizzata e i listener appropriati.

Per aggiungere il supporto VPAID 2.0:

1. Aggiungere la visualizzazione annunci personalizzata all&#39;interfaccia del lettore.

   ```java
   _playerFrame.addView(mediaPlayer.createCustomAdView());
   ```

1. Aggiunta di un listener per gli eventi di annunci personalizzati.

   ```java
   mediaplayer.addEventListener(MediaPlayer.Event.CUSTOM_AD,  
     _customAdEventListener);
   ```

