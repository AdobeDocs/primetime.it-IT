---
description: Per aggiungere il supporto VPAID 2.0, aggiungi una visualizzazione annuncio personalizzata e i listener appropriati.
title: Implementazione dell’integrazione VPAID 2.0
exl-id: 8a6b81e7-1034-48fc-87aa-4cb8ab305d15
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---

# Implementazione dell’integrazione VPAID 2.0 {#implement-vpaid-integration}

Per aggiungere il supporto VPAID 2.0, aggiungi una visualizzazione annuncio personalizzata e i listener appropriati.

Per aggiungere il supporto VPAID 2.0:

1. Aggiungi la visualizzazione personalizzata dell’annuncio all’interfaccia del lettore quando questo si trova nello stato PREPARATO.

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

1. Creare listener ed elaborare gli eventi descritti in listener di eventi.

   >[!IMPORTANT]
   >
   >In un flusso di lavoro VPAID 2.0, per le visualizzazioni di annunci personalizzate è molto importante mantenere `CustomAdView` istanza in `AdBreak` starts (evento) `AD_BREAK_START`) e `AdBreak` completes (evento `AD_BREAK_COMPLETE`), dal momento della creazione della visualizzazione dell’annuncio personalizzata fino al momento dello smaltimento. In altre parole, non creare una visualizzazione personalizzata a ogni avvio dell’interruzione pubblicitaria ed eliminarla a ogni interruzione pubblicitaria completata.
   >
   >
   >Inoltre, è necessario creare la visualizzazione dell’annuncio personalizzato solo quando il lettore è nello stato PREPARATO,
   >
   >
   >Elimina la visualizzazione dell’annuncio personalizzato solo quando viene chiamato il ripristino. Ad esempio:
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
   >Infine, prima di eliminare la visualizzazione dell’annuncio personalizzata, devi rimuoverla dal `FrameLayout`. Ad esempio:
   >
   >
   ```
   >if (_playerFrame != null) 
   >       _playerFrame.removeAllViews(); 
   >```
