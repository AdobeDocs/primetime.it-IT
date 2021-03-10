---
description: Per aggiungere il supporto VPAID 2.0, aggiungi una visualizzazione annunci personalizzata e gli ascoltatori appropriati.
title: Implementare l’integrazione con VPAID 2.0
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 2%

---


# Implementare l&#39;integrazione VPAID 2.0 {#implement-vpaid-integration}

Per aggiungere il supporto VPAID 2.0, aggiungi una visualizzazione annunci personalizzata e gli ascoltatori appropriati.

1. Aggiungi la visualizzazione annunci personalizzata all&#39;interfaccia del lettore quando il lettore è nello stato PREPARATO.

   ```java
   ... 
   private FrameLayout _playerFrame; 
       ... 
       case PREPARED: 
           ... 
           addCustomView(); 
   ... 
   private void addCustomView() { 
       ... 
       WebView view = (WebView)_mediaPlayer.getCustomAdView(); 
       ... 
       _playerFrame.addView(view);
   ```

1. Crea i listener ed elabora gli eventi descritti in [Eventi](../../../../tvsdk-3x-android-prog/android-3x-events-notifications/events-summary/android-3x-events-summary.md).

   >[!IMPORTANT]
   >
   >In un flusso di lavoro VPAID 2.0, per le visualizzazioni di annunci personalizzate è molto importante mantenere l’istanza `CustomAdView` tra `AdBreak` gli avvii (evento `AD_BREAK_START`) e le visualizzazioni di `AdBreak` completate (evento `AD_BREAK_COMPLETE`), dal momento in cui crei la visualizzazione di annunci personalizzata fino a quando la elimini. Cioè, non creare una visualizzazione annunci personalizzata su ogni inizio di interruzione annuncio e disporla su ogni interruzione annuncio completata.
   >
   >
   >Inoltre, devi creare la visualizzazione annunci personalizzata solo quando il lettore è nello stato PREPARATO,
   >
   >
   >Quando viene chiamata la reimpostazione, elimina la visualizzazione annunci personalizzata solo. Ad esempio:
   >
   >
   ```
   >// on reset 
   >if (_mediaPlayer != null) { 
   >       _mediaPlayer.disposeCustomAdView(); 
   >       ... 
   >} 
   >
   >```
   >
   >Infine, prima di eliminare la visualizzazione annunci personalizzata, devi rimuoverla dal `FrameLayout`. Ad esempio:
   >
   >
   ```
   >if (_playerFrame != null) 
   >       _playerFrame.removeAllViews(); 
   >```
