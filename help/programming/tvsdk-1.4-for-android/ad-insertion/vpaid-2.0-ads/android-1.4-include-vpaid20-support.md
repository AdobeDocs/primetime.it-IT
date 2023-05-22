---
description: Per aggiungere il supporto VPAID 2.0, aggiungi una visualizzazione annuncio personalizzata e i listener appropriati.
title: Implementazione dell’integrazione VPAID 2.0
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '50'
ht-degree: 0%

---


# Implementazione dell’integrazione VPAID 2.0{#implement-vpaid-integration}

Per aggiungere il supporto VPAID 2.0, aggiungi una visualizzazione annuncio personalizzata e i listener appropriati.

Per aggiungere il supporto VPAID 2.0:

1. Aggiungi la visualizzazione annuncio personalizzata all’interfaccia del lettore.

   ```java
   _playerFrame.addView(mediaPlayer.createCustomAdView());
   ```

1. Aggiungi un listener per gli eventi annuncio personalizzati.

   ```java
   mediaplayer.addEventListener(MediaPlayer.Event.CUSTOM_AD,  
     _customAdEventListener);
   ```

