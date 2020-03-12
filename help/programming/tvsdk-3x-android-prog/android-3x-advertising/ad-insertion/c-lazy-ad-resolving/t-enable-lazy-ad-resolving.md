---
description: Potete attivare o disattivare la funzione Lazy Ad Resolving utilizzando il meccanismo di caricamento Lazy Ad esistente (Lazy Ad Resolving è disabilitato per impostazione predefinita).
keywords: Lazy;Ad resolving;Ad loading;delayLoading
seo-description: Potete attivare o disattivare la funzione Lazy Ad Resolving utilizzando il meccanismo di caricamento Lazy Ad esistente (Lazy Ad Resolving è disabilitato per impostazione predefinita).
seo-title: Abilita risoluzione annunci pigri
title: Abilita risoluzione annunci pigri
uuid: 91884eea-a622-4f5d-b6a8-36bb0050ba1d
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Abilita risoluzione annunci pigri {#enable-lazy-ad-resolving}

Potete attivare o disattivare la funzione Lazy Ad Resolving utilizzando il meccanismo di caricamento Lazy Ad esistente (Lazy Ad Resolving è disabilitato per impostazione predefinita).

Potete abilitare o disabilitare la risoluzione degli annunci pigri chiamando [AdvertisingMetadata.setDelayLoading](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/com/adobe/mediacore/metadata/AdvertisingMetadata.html#setDelayAdLoading-boolean-) con true o false.

* Utilizzate i metodi booleani *hasDelayAdLoading* e *setDelayAdLoading* in AdvertisingMetadata per controllare il tempo di risoluzione degli annunci e il posizionamento degli annunci sulla timeline:

   * Se *hasDelayAdLoading* restituisce false, TVSDK attende che tutti gli annunci vengano risolti e inseriti prima di passare allo stato PREPARATO.
   * Se *hasDelayAdLoading* restituisce true, TVSDK risolve solo gli annunci e le transizioni iniziali allo stato PREPARED.

      * Gli altri annunci vengono risolti e inseriti durante la riproduzione.
   * Se *hasPreroll *o *hasLivePreroll* restituisce false, TVSDK presuppone che non sia presente alcun annuncio preroll e avvia immediatamente la riproduzione del contenuto. Questi valori predefiniti sono impostati su true.


**API rilevanti per la risoluzione degli annunci pigri:**

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

Per riflettere con precisione gli annunci come segnali su una barra di scorrimento, ascoltate l’ `TimelineEvent`evento e ridisegnate la barra di scorrimento ogni volta che ricevete questo evento.

Quando Lazy Ad Resolving è abilitato per i flussi VOD, tutte le interruzioni di annuncio vengono inserite nella timeline, tuttavia, molte delle interruzioni di annuncio non verranno ancora risolte. L’applicazione può determinare se disegnare o meno questi marcatori controllando il `TimelineMarker::getDuration()`. Se il valore è maggiore di zero, gli annunci all&#39;interno dell&#39;interruzione di annuncio sono stati risolti.

TVSDK invia questo evento quando è stata risolta un&#39;interruzione pubblicitaria, e anche quando il lettore passa allo stato PREPARATO.

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
