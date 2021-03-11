---
description: Puoi abilitare o disabilitare la funzione Lazy Ad Resolving utilizzando il meccanismo esistente Lazy Ad Loading (Lazy Ad Resolving è disabilitato per impostazione predefinita).
keywords: Pigro;risoluzione annunci;Caricamento annunci;ritardoLoading
title: Abilita risoluzione annunci pigri
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 0%

---


# Abilita risoluzione annunci pigri {#enable-lazy-ad-resolving}

Puoi abilitare o disabilitare la funzione Lazy Ad Resolving utilizzando il meccanismo esistente Lazy Ad Loading (Lazy Ad Resolving è disabilitato per impostazione predefinita).

Puoi abilitare o disabilitare Lazy Ad Resolving richiamando [AdvertisingMetadata.setDelayLoading](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/com/adobe/mediacore/metadata/AdvertisingMetadata.html#setDelayAdLoading-boolean-) con true o false.

* Utilizza i metodi booleani *hasDelayAdLoading* e *setDelayAdLoading* in AdvertisingMetadata per controllare la tempistica della risoluzione degli annunci e il posizionamento degli annunci sulla timeline:

   * Se *hasDelayAdLoading* restituisce false, TVSDK attende che tutti gli annunci vengano risolti e inseriti prima di passare allo stato PREPARED.
   * Se *hasDelayAdLoading* restituisce true, TVSDK risolve solo gli annunci e le transizioni iniziali allo stato PREPARATO.

      * Gli annunci rimanenti vengono risolti e inseriti durante la riproduzione.
   * Se *hasPreroll *o *hasLivePreroll* restituisce false, TVSDK presuppone che non vi sia alcun annuncio preliminare e avvia immediatamente la riproduzione del contenuto. Queste sono impostate su true per impostazione predefinita.


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

Per riflettere con precisione gli annunci come indizi su una barra di scorrimento, ascolta l’evento `TimelineEvent`e ridisegna la barra di scorrimento ogni volta che ricevi questo evento.

Quando Lazy Ad Resolving è abilitato per flussi VOD, tutte le interruzioni di annunci vengono posizionate sulla timeline, tuttavia, molte interruzioni di annunci non saranno ancora risolte. L&#39;applicazione può determinare se disegnare o meno questi marcatori controllando `TimelineMarker::getDuration()`. Se il valore è maggiore di zero, gli annunci all’interno dell’interruzione pubblicitaria sono stati risolti.

TVSDK invia questo evento quando un&#39;interruzione pubblicitaria è stata risolta e anche quando il lettore passa allo stato PREPARED.

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
