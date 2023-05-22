---
description: Puoi abilitare o disabilitare la funzione Lazy Ad Resolving utilizzando il meccanismo esistente Lazy Ad Loading (Lazy Ad Resolving è abilitato per impostazione predefinita).
keywords: Lazy;Risoluzione annuncio;Caricamento annuncio;delayLoading
title: Abilita lazy ad resolving
exl-id: 4cd53ace-b0f5-4eef-93c3-644c2f48ce49
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 0%

---

# Abilita lazy ad resolving {#enable-lazy-ad-resolving}

Puoi abilitare o disabilitare la funzione Lazy Ad Resolving utilizzando il meccanismo esistente Lazy Ad Loading (Lazy Ad Resolving è abilitato per impostazione predefinita).

Puoi abilitare o disabilitare Lazy Ad Resolving chiamando [AdvertisingMetadata.setDelayLoading](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/com/adobe/mediacore/metadata/AdvertisingMetadata.html#setDelayAdLoading-boolean-) con `true` o `false`.

1. Utilizza il valore booleano `hasDelayAdLoading` e `setDelayAdLoading` metodi in `AdvertisingMetadata` per controllare la tempistica della risoluzione degli annunci e il posizionamento degli annunci sulla timeline:

   * Se `hasDelayAdLoading` restituisce false. TVSDK attende che tutti gli annunci vengano risolti e posizionati prima di passare allo stato PREPARATO.
   * Se `hasDelayAdLoading` restituisce true, TVSDK risolve solo gli annunci e le transizioni iniziali nello stato PREPARATO. Gli annunci rimanenti vengono risolti e posizionati durante la riproduzione.
   * Quando `hasPreroll` o `hasLivePreroll` return false, TVSDK presuppone che non vi sia alcun annuncio preroll e avvia immediatamente la riproduzione del contenuto. Per impostazione predefinita sono true.

      API rilevanti per la risoluzione lazy degli annunci:

      ```
      Class: 
         com.adobe.mediacore.metadata.AdvertisingMetadata 
      
      Methods: 
      […] 
          public final boolean hasDelayAdLoading() // Check if Lazy Ad Resolving enabled 
          public final void setDelayAdLoading()    // Enable or disable Lazy Ad Resolving 
          public final boolean hasPreroll()        // Check for existence of pre-roll ads 
          public final void setPreroll()           // Set pre-roll true or false 
          public final boolean hasLivePreroll()    // Check for live pre-roll ads 
          public final void setLivePreroll()       // Set live pre-roll true or false 
      […]
      ```

1. Per riflettere accuratamente gli annunci come spunti su una barra di scorrimento, ascolta la `TimelineEvent` e ridisegnare la barra di scorrimento ogni volta che si riceve questo evento.

   Quando Lazy Ad Resolving è abilitato per i flussi VOD, non tutti gli annunci vengono inseriti nella timeline quando il lettore entra nello stato READY, pertanto il lettore deve ridisegnare esplicitamente la barra di scorrimento.

   TVSDK ottimizza l’invio di questo evento per ridurre al minimo il numero di volte in cui è necessario ridisegnare la barra di scorrimento; pertanto, il numero di eventi della timeline non è correlato al numero di interruzioni pubblicitarie da posizionare sulla timeline. Ad esempio, in presenza di cinque interruzioni pubblicitarie, potresti non ricevere esattamente cinque eventi.

   ```java
   mediaPlayer.addEventListener 
       (MediaPlayerEvent.TIMELINE_UPDATED, timelineUpdatedEventListener); 
   /** 
    * ... 
    */ 
   public void onTimelineUpdated(TimelineEvent event) { 
   
       for (PlaybackManagerEventListener listener : eventListeners) { 
           listener.onUpdate(getLocalSeekRange(), event.getTimeline()); 
       } 
   } 
   ```

>Per verificare se la funzione Lazy Ad Resolving è abilitata o disabilitata, chiama `AdvertisingMetadata.hasDelayAdLoading`. Un valore restituito di `true` significa che è abilitato il Lazy Ad Resolving; `false` significa che la funzione è disabilitata.
