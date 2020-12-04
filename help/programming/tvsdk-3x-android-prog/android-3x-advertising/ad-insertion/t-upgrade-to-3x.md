---
description: 'L''interfaccia com.adobe.mediacore.timeline.TimelineMarker ora contiene un nuovo metodo '
seo-description: 'L''interfaccia com.adobe.mediacore.timeline.TimelineMarker ora contiene un nuovo metodo '
seo-title: 'Aggiornamento da 2.5.x Lazy Ad Resolving a 3.0.0 Lazy Ad Resolving (modifiche API/Flusso di lavoro) '
title: 'Aggiornamento da 2.5.x Lazy Ad Resolving a 3.0.0 Lazy Ad Resolving (modifiche API/Flusso di lavoro) '
uuid: 5870ceb4-93a8-4c8b-b716-673396122644
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 0%

---


# Aggiornamento da 2.5.x Lazy Ad Resolving a 3.x Lazy Ad Resolving (modifiche API/Flusso di lavoro):{#upgrading-from-x-lazy-ad-resolving-to-lazy-ad-resolving-api-workflow-changes}

L&#39;interfaccia com.adobe.mediacore.timeline.TimelineMarker ora contiene un nuovo metodo:

**Placement.Type getPlacementType()**

Questo metodo restituisce un tipo di posizionamento di Placement.Type.PRE_ROLL, Placement.Type.MID_ROLL o Placement.Type.POST_ROLL. Se un&#39;interruzione di annuncio non viene risolta, il metodo `getDuration()`nell&#39;interfaccia TimelineMarker restituirà 0.

>[!NOTE]
>
>Questa interfaccia non viene sempre inserita nel tipo com.mediacore.timeline.advertising.AdBreakTimelineItem se non è ancora stata risolta. Sarà possibile eseguire l&#39;inserimento se il metodo `getDuration()` di TimelineMarker è maggiore di 0.

**Modifiche all&#39;evento:**

`kEventAdResolutionComplete` ora viene ammortizzato e ora viene attivato subito dopo che il lettore entra nello stato PREPARATO. Le applicazioni che in precedenza ascoltavano solo questo evento per disegnare la barra di scorrimento devono modificare questo valore in modo da poter ascoltare solo `kEventTimelineUpdated`. Dopo la risoluzione di singole interruzioni pubblicitarie, viene inviato un nuovo evento `kEventTimelineUpdated`.
