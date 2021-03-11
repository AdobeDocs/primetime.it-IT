---
description: Puoi abilitare o disabilitare la funzione Lazy Ad Resolving utilizzando il meccanismo esistente Lazy Ad Loading (Lazy Ad Resolving è abilitato per impostazione predefinita).
keywords: Pigro;risoluzione annunci;Caricamento annunci;ritardoLoading
title: Abilita risoluzione annunci pigri
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 0%

---


# Abilita risoluzione annunci pigri {#enable-lazy-ad-resolving}

Puoi abilitare o disabilitare la funzione Lazy Ad Resolving utilizzando il meccanismo esistente Lazy Ad Loading (Lazy Ad Resolving è abilitato per impostazione predefinita).

Puoi abilitare o disabilitare Lazy Ad Resolving richiamando [AdvertisingMetadata.setDelayLoading](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/com/adobe/mediacore/metadata/AdvertisingMetadata.html#setDelayAdLoading-boolean-) con `true` o `false`.

1. Utilizza i metodi booleani `hasDelayAdLoading` e `setDelayAdLoading` in `AdvertisingMetadata` per controllare la tempistica della risoluzione degli annunci e il posizionamento degli annunci sulla timeline:

   * Se `hasDelayAdLoading` restituisce false, TVSDK attende che tutti gli annunci vengano risolti e inseriti prima di passare allo stato PREPARED.
   * Se `hasDelayAdLoading` restituisce true, TVSDK risolve solo gli annunci e le transizioni iniziali allo stato PREPARATO. Gli annunci rimanenti vengono risolti e inseriti durante la riproduzione.
   * Quando `hasPreroll` o `hasLivePreroll` restituisce false, TVSDK presuppone che non sia presente alcun annuncio preliminare e avvia immediatamente la riproduzione del contenuto. Questi valori predefiniti sono true.

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

1. Per riflettere con precisione gli annunci come indizi su una barra di scorrimento, ascolta l’evento `TimelineEvent` e ridisegna la barra di scorrimento ogni volta che ricevi questo evento.

   Quando Lazy Ad Resolving è abilitato per flussi VOD, non tutti gli annunci vengono inseriti sulla timeline quando il lettore entra nello stato PREPARATO, in modo che il lettore debba ridisegnare esplicitamente la barra di scorrimento.

   TVSDK ottimizza l’invio di questo evento per ridurre al minimo il numero di volte in cui è necessario ridisegnare la barra di scorrimento; pertanto, il numero di eventi della timeline non è correlato al numero di interruzioni pubblicitarie da inserire nella timeline. Ad esempio, in presenza di cinque interruzioni pubblicitarie, potresti non ricevere esattamente cinque eventi.

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

>Per verificare se la funzione Lazy Ad Resolving è abilitata o disabilitata, chiama `AdvertisingMetadata.hasDelayAdLoading`. Un valore restituito di `true` indica che Lazy Ad Resolving è abilitato; `false` indica che la funzione è disabilitata.

