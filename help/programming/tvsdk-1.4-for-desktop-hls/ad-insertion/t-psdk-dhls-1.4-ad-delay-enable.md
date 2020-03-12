---
description: Potete specificare se consentire la riproduzione prima che tutti gli annunci vengano caricati e inseriti nella timeline. L’avvio della riproduzione in questo modo consente a un visualizzatore di accedere più rapidamente al contenuto principale. Questa funzione è applicabile solo per i DVR live e non funziona, ad esempio, sulle risorse VOD.
seo-description: Potete specificare se consentire la riproduzione prima che tutti gli annunci vengano caricati e inseriti nella timeline. L’avvio della riproduzione in questo modo consente a un visualizzatore di accedere più rapidamente al contenuto principale. Questa funzione è applicabile solo per i DVR live e non funziona, ad esempio, sulle risorse VOD.
seo-title: Abilitare il caricamento di annunci pigri
title: Abilitare il caricamento di annunci pigri
uuid: ac7c8801-7fa2-4f17-b79c-c603b3236948
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Abilitare il caricamento di annunci pigri{#enable-lazy-ad-loading}

Potete specificare se consentire la riproduzione prima che tutti gli annunci vengano caricati e inseriti nella timeline. L’avvio della riproduzione in questo modo consente a un visualizzatore di accedere più rapidamente al contenuto principale. Questa funzione è applicabile solo per i DVR live e non funziona, ad esempio, sulle risorse VOD.

1. Utilizzare la proprietà booleana `delayAdLoading` in `AdvertisingMetadata`.

   * Se è false, TVSDK attende che tutti gli annunci vengano risolti e inseriti prima di passare allo stato PREPARATO. Per impostazione predefinita è false.
   * Se true, TVSDK risolve solo gli annunci iniziali e le transizioni allo stato PREPARATO. Gli altri annunci vengono risolti e inseriti durante la riproduzione.

1. Per attivare anche il caricamento ritardato degli annunci con Adobe Primetime e la decisione degli annunci, imposta questo valore al `true` momento della creazione `AuditudeSettings`.

   La `AuditudeSettings` classe eredita questa proprietà da `AdvertisingMetadata`, ma non eredita il valore corrente.

   ```
   var auditudeSettings:AuditudeSettings = new AuditudeSettings(); 
   auditudeSettings.mediaId = ... 
   auditudeSettings.zoneId = ... 
   auditudeSettings.delayAdLoading = true;
   ```

1. Per riflettere con precisione gli annunci come segnali su una barra di scorrimento, ascoltate il `TimelineEvent`. `TIMELINE_UPDATED` e ridisegnate la barra di scorrimento ogni volta che ricevete questo evento.

   Quando i flussi VoD utilizzano il caricamento ritardato degli annunci, non tutti gli annunci vengono inseriti nella timeline quando il lettore entra nello stato PREPARATO, pertanto devi ridisegnare esplicitamente la barra di scorrimento.

   TVSDK ottimizza l&#39;invio di questo evento per ridurre al minimo il numero di volte che è necessario ridisegnare la barra di scorrimento; pertanto, il numero di eventi della timeline non è correlato al numero di interruzioni pubblicitarie da inserire nella timeline. Ad esempio, se hai cinque interruzioni pubblicitarie, potresti non ricevere esattamente cinque eventi.

   ```
   mediaPlayer.addEventListener(TimelineEvent.TIMELINE_UPDATED, onTimelineUpdated); 
   // ... 
   function onTimelineUpdated(event:TimelineEvent):void { 
       // get markers 
       var markers:Vector.<TimelineMarker> = event.timeline.timelineMarkers; 
       drawMarkers(markers); 
   } 
   ```

