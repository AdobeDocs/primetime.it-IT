---
description: Puoi specificare se consentire la riproduzione prima che tutti gli annunci vengano caricati e posizionati nella timeline. Avviando la riproduzione in questo modo, l’utente può accedere più rapidamente al contenuto principale. Questa funzione è applicabile solo ai DVR live e non funziona, ad esempio, con le risorse VOD.
title: Attiva il caricamento lento degli annunci
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# Attiva il caricamento lento degli annunci{#enable-lazy-ad-loading}

Puoi specificare se consentire la riproduzione prima che tutti gli annunci vengano caricati e posizionati nella timeline. Avviando la riproduzione in questo modo, l’utente può accedere più rapidamente al contenuto principale. Questa funzione è applicabile solo ai DVR live e non funziona, ad esempio, con le risorse VOD.

1. Utilizzare la proprietà booleana `delayAdLoading` in `AdvertisingMetadata`.

   * Se è false, TVSDK attende che tutti gli annunci siano risolti e posizionati prima di passare allo stato PREPARATO. È false per impostazione predefinita.
   * Se è true, TVSDK risolve solo gli annunci iniziali e le transizioni nello stato PREPARATO. Gli annunci rimanenti vengono risolti e posizionati durante la riproduzione.

1. Per attivare anche il caricamento ritardato degli annunci con Adobe Primetime ad decisioning, imposta questo su `true` quando si crea `AuditudeSettings`.

   Il `AuditudeSettings` la classe eredita questa proprietà da `AdvertisingMetadata`, ma non eredita il valore corrente.

   ```
   var auditudeSettings:AuditudeSettings = new AuditudeSettings(); 
   auditudeSettings.mediaId = ... 
   auditudeSettings.zoneId = ... 
   auditudeSettings.delayAdLoading = true;
   ```

1. Per riflettere accuratamente gli annunci come spunti su una barra di scorrimento, ascolta la `TimelineEvent`. `TIMELINE_UPDATED` e ridisegnare la barra di scorrimento ogni volta che si riceve questo evento.

   Quando i flussi VoD utilizzano il caricamento ritardato degli annunci, non tutti gli annunci vengono inseriti sulla timeline quando il lettore entra nello stato READY, pertanto è necessario ridisegnare esplicitamente la barra di scorrimento.

   TVSDK ottimizza l’invio di questo evento per ridurre al minimo il numero di volte in cui è necessario ridisegnare la barra di scorrimento; pertanto, il numero di eventi della timeline non è correlato al numero di interruzioni pubblicitarie da posizionare sulla timeline. Ad esempio, in presenza di cinque interruzioni pubblicitarie, potresti non ricevere esattamente cinque eventi.

   ```
   mediaPlayer.addEventListener(TimelineEvent.TIMELINE_UPDATED, onTimelineUpdated); 
   // ... 
   function onTimelineUpdated(event:TimelineEvent):void { 
       // get markers 
       var markers:Vector.<TimelineMarker> = event.timeline.timelineMarkers; 
       drawMarkers(markers); 
   } 
   ```
