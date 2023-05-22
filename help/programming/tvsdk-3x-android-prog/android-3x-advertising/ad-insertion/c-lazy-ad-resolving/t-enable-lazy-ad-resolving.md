---
description: Puoi abilitare o disabilitare la funzione Lazy Ad Resolving utilizzando il meccanismo esistente Lazy Ad Loading (Lazy Ad Resolving è disabilitato per impostazione predefinita).
keywords: Lazy;Risoluzione annuncio;Caricamento annuncio;delayLoading
title: Abilita lazy ad resolving
exl-id: a52a1f9a-3bf6-4193-8347-1ef248ba8884
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 0%

---

# Abilita lazy ad resolving {#enable-lazy-ad-resolving}

Puoi abilitare o disabilitare la funzione Lazy Ad Resolving utilizzando il meccanismo esistente Lazy Ad Loading (Lazy Ad Resolving è disabilitato per impostazione predefinita).

Puoi abilitare o disabilitare Lazy Ad Resolving chiamando [AdvertisingMetadata.setDelayLoading](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/com/adobe/mediacore/metadata/AdvertisingMetadata.html#setDelayAdLoading-boolean-) con true o false.

* Utilizza il valore booleano *hasDelayAdLoading* e *setDelayAdLoading* metodi in AdvertisingMetadata per controllare la tempistica della risoluzione degli annunci e il posizionamento degli annunci sulla timeline:

   * Se *hasDelayAdLoading* restituisce false. TVSDK attende che tutti gli annunci vengano risolti e posizionati prima di passare allo stato PREPARATO.
   * Se *hasDelayAdLoading* restituisce true, TVSDK risolve solo gli annunci e le transizioni iniziali nello stato PREPARATO.

      * Gli annunci rimanenti vengono risolti e posizionati durante la riproduzione.
   * Se *ha Preroll *o *hasLivePreroll* return false, TVSDK presuppone che non vi sia alcun annuncio preroll e avvia immediatamente la riproduzione del contenuto. Questi sono impostati per impostazione predefinita su true.


**API rilevanti per la risoluzione lazy degli annunci:**

```
Class:    com.adobe.mediacore.metadata.AdvertisingMetadata 
Methods: 
    public final boolean hasDelayAdLoading() // Check if Lazy Ad Resolving enabled 
    public final void setDelayAdLoading() // Enable or disable Lazy Ad Resolving 
    public final void setDelayAdLoadingTolerance() // Sets the Lazy Ad Resolving Tolerance level.  This value is added to the BufferControlParameters::playBufferTime and the content's EXT-X-TARGETDURATION to determine when ad breaks should resolve 
    public final double getDelayAdLoadingTolerance() // Gets the Lazy Ad Resolving Tolerance level 
    public final boolean hasPreroll() // Check for existence of pre-roll ads 
    public final void setPreroll() // Set pre-roll true or false 
    public final boolean hasLivePreroll() // Check for live pre-roll ads 
    public final void setLivePreroll() // Set live pre-roll true or false

Class:     com.adobe.mediacore.timeline.TimelineMarker 
Methods: 
    public double getDuration() // Returns the current duration of the TimelineMarker.  This will be zero if the ad break has not yet resolved. 
    public Placement.Type getPlacementType() // Returns whether
```

Per riflettere accuratamente gli annunci come spunti su una barra di scorrimento, ascolta la `TimelineEvent`e ridisegnare la barra di scorrimento ogni volta che si riceve questo evento.

Quando la funzione Lazy Ad Resolving è abilitata per i flussi VOD, tutte le interruzioni pubblicitarie vengono posizionate sulla timeline; tuttavia, molte delle interruzioni pubblicitarie non saranno ancora risolte. L&#39;applicazione può determinare se disegnare o meno questi marcatori controllando `TimelineMarker::getDuration()`. Se il valore è maggiore di zero, gli annunci all’interno dell’interruzione pubblicitaria sono stati risolti.

TVSDK invia questo evento quando un’interruzione pubblicitaria è stata risolta e anche quando il lettore passa allo stato PREPARATO.

```
mediaPlayer.addEventListener(MediaPlayerEvent.TIMELINE_UPDATED, timelineUpdatedEventListener); 
/** 
* ... 
*/ 
public void onTimelineUpdated(TimelineEvent event) { 
for (PlaybackManagerEventListener listener : eventListeners) { 
  listener.onUpdate(getLocalSeekRange(), event.getTimeline()); 
}
```
