---
description: È possibile specificare se consentire la riproduzione prima che tutti gli annunci vengano caricati e inseriti nella timeline. La riproduzione viene avviata in modo da consentire a un visualizzatore di accedere più rapidamente al contenuto principale. Questa funzione è applicabile solo per il DVR live e non funziona, ad esempio, su VOD assets.
title: Abilita il caricamento lento degli annunci
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---


# Abilita il caricamento lento degli annunci{#enable-lazy-ad-loading}

È possibile specificare se consentire la riproduzione prima che tutti gli annunci vengano caricati e inseriti nella timeline. La riproduzione viene avviata in modo da consentire a un visualizzatore di accedere più rapidamente al contenuto principale. Questa funzione è applicabile solo per il DVR live e non funziona, ad esempio, su VOD assets.

1. Utilizzare la proprietà booleana `delayAdLoading` in `AdvertisingMetadata`.

   * Se false, TVSDK attende che tutti gli annunci vengano risolti e inseriti prima di passare allo stato PREPARED. È false per impostazione predefinita.
   * Se true, TVSDK risolve solo gli annunci e le transizioni iniziali allo stato PREPARATO. Gli annunci rimanenti vengono risolti e inseriti durante la riproduzione.

1. Per attivare anche il caricamento ritardato degli annunci con Adobe Primetime ad decision, imposta questo su `true` quando crei `AuditudeSettings`.

   La classe `AuditudeSettings` eredita questa proprietà da `AdvertisingMetadata`, ma non eredita il valore corrente.

   ```
   var auditudeSettings:AuditudeSettings = new AuditudeSettings(); 
   auditudeSettings.mediaId = ... 
   auditudeSettings.zoneId = ... 
   auditudeSettings.delayAdLoading = true;
   ```

1. Per riflettere con precisione gli annunci come indizi su una barra di scorrimento, ascolta la sezione `TimelineEvent`. `TIMELINE_UPDATED` e ridisegnare la barra di scorrimento ogni volta che si riceve questo evento.

   Quando i flussi VoD utilizzano il caricamento ritardato degli annunci, non tutti gli annunci vengono inseriti sulla timeline quando il lettore entra nello stato PREPARATO, quindi devi ridisegnare esplicitamente la barra di scorrimento.

   TVSDK ottimizza l’invio di questo evento per ridurre al minimo il numero di volte in cui è necessario ridisegnare la barra di scorrimento; pertanto, il numero di eventi della timeline non è correlato al numero di interruzioni pubblicitarie da inserire nella timeline. Ad esempio, in presenza di cinque interruzioni pubblicitarie, potresti non ricevere esattamente cinque eventi.

   ```
   mediaPlayer.addEventListener(TimelineEvent.TIMELINE_UPDATED, onTimelineUpdated); 
   // ... 
   function onTimelineUpdated(event:TimelineEvent):void { 
       // get markers 
       var markers:Vector.<TimelineMarker> = event.timeline.timelineMarkers; 
       drawMarkers(markers); 
   } 
   ```

