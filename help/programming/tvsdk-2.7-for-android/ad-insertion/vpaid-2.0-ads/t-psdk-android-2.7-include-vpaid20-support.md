---
description: Per aggiungere il supporto VPAID 2.0, aggiungi una visualizzazione ad personalizzata e i listener appropriati.
seo-description: Per aggiungere il supporto VPAID 2.0, aggiungi una visualizzazione ad personalizzata e i listener appropriati.
seo-title: Implementare l'integrazione VPAID 2.0
title: Implementare l'integrazione VPAID 2.0
uuid: fa5b9cdd-e684-4656-91b7-50781dc59e23
translation-type: tm+mt
source-git-commit: 25f97c8d296f71deddc8f9d12b97007ddf73f603
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 2%

---


# Implementare l&#39;integrazione VPAID 2.0 {#implement-vpaid-integration}

Per aggiungere il supporto VPAID 2.0, aggiungi una visualizzazione ad personalizzata e i listener appropriati.

Per aggiungere il supporto VPAID 2.0:

1. Aggiungere la visualizzazione ad personalizzata all&#39;interfaccia del lettore quando il lettore è nello stato PREPARATO.

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

1. Creare listener ed elaborare gli eventi descritti nei listener di eventi.

   >[!IMPORTANT]
   >
   >In un flusso di lavoro VPAID 2.0, per le visualizzazioni di annunci personalizzate è molto importante mantenere l&#39;istanza `CustomAdView` tra `AdBreak` avvii (evento `AD_BREAK_START`) e `AdBreak` completati (evento `AD_BREAK_COMPLETE`), dal momento in cui create la visualizzazione di annunci personalizzata fino al momento in cui la eliminate. Ovvero, non create una visualizzazione annunci personalizzata per ogni inizio di interruzione e non eliminatela per ogni interruzione di annuncio completata.
   >
   >
   >Inoltre, è consigliabile creare la visualizzazione annunci personalizzata solo quando il lettore è nello stato PREPARATO,
   >
   >
   >Eliminate la visualizzazione annunci personalizzata solo quando viene chiamato il ripristino. Ad esempio:
   >
   >
   ```
   >// on reset 
   >if (_mediaPlayer != null) { 
   >       _mediaPlayer.disposeCustomAdView(); 
   >       ... 
   >} 
   >```
   >
   >Infine, prima di eliminare la visualizzazione personalizzata dell&#39;annuncio, è necessario rimuoverla dall&#39; `FrameLayout`. Ad esempio:
   >
   >
   ```
   >if (_playerFrame != null) 
   >       _playerFrame.removeAllViews(); 
   >```
