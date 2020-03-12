---
description: Potete attivare o disattivare la funzione Lazy Ad Resolving utilizzando il meccanismo di caricamento Lazy Ad esistente (Lazy Ad Resolving è attivato per impostazione predefinita).
keywords: Lazy;Ad resolving;Ad loading;delayLoading
seo-description: Potete attivare o disattivare la funzione Lazy Ad Resolving utilizzando il meccanismo di caricamento Lazy Ad esistente (Lazy Ad Resolving è attivato per impostazione predefinita).
seo-title: Abilita risoluzione annunci pigri
title: Abilita risoluzione annunci pigri
uuid: a084ee0b-53af-4600-91f6-d30ccc89699d
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# Abilita risoluzione annunci pigri {#enable-lazy-ad-resolving}

Potete attivare o disattivare la funzione Lazy Ad Resolving utilizzando il meccanismo di caricamento Lazy Ad esistente (Lazy Ad Resolving è attivato per impostazione predefinita).

Puoi abilitare o disabilitare la risoluzione degli annunci pigri chiamando [AdvertisingMetadata.setDelayLoading](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/com/adobe/mediacore/metadata/AdvertisingMetadata.html#setDelayAdLoading-boolean-) con `true` o `false`.

1. Utilizzate i metodi booleani `hasDelayAdLoading` e `setDelayAdLoading` metodi in `AdvertisingMetadata` per controllare la tempistica della risoluzione degli annunci e il posizionamento degli annunci sulla timeline:

   * Se `hasDelayAdLoading` restituisce false, TVSDK attende che tutti gli annunci vengano risolti e inseriti prima di passare allo stato PREPARATO.
   * Se `hasDelayAdLoading` restituisce true, TVSDK risolve solo gli annunci e le transizioni iniziali allo stato PREPARATO. Gli altri annunci vengono risolti e inseriti durante la riproduzione.
   * Se `hasPreroll` o `hasLivePreroll` restituisce false, TVSDK presuppone che non sia presente alcun annuncio pubblicitario e avvia immediatamente la riproduzione del contenuto. Il valore predefinito è true.

      API rilevanti per la risoluzione degli annunci pigri:

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

1. Per riflettere con precisione gli annunci come segnali su una barra di scorrimento, ascoltate l&#39; `TimelineEvent` evento e ridisegnate la barra di scorrimento ogni volta che ricevete questo evento.

   Quando Lazy Ad Resolving è abilitato per i flussi VOD, non tutti gli annunci vengono inseriti nella timeline quando il lettore entra nello stato PREPARATO, pertanto il lettore deve ridisegnare esplicitamente la barra di scorrimento.

   TVSDK ottimizza l&#39;invio di questo evento per ridurre al minimo il numero di volte che è necessario ridisegnare la barra di scorrimento; pertanto, il numero di eventi della timeline non è correlato al numero di interruzioni pubblicitarie da inserire nella timeline. Ad esempio, se hai cinque interruzioni pubblicitarie, potresti non ricevere esattamente cinque eventi.

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

>Per verificare se la funzione Lazy Ad Resolving è abilitata o disabilitata, chiamate `AdvertisingMetadata.hasDelayAdLoading`. Un valore restituito `true` indica che è abilitata la funzione Lazy Ad Resolving; significa `false` che la funzione è disabilitata.

