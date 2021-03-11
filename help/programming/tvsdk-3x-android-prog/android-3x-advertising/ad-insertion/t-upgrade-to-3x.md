---
description: 'L''interfaccia com.adobe.mediacore.timeline.TimelineMarker contiene ora un nuovo metodo '
title: 'Aggiornamento da Risoluzione annunci Lazy 2.5.x a Risoluzione annunci Lazy 3.0.0 (modifiche API/Flusso di lavoro) '
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---


# Aggiornamento da Risoluzione annunci Lazy 2.5.x a Risoluzione annunci Lazy 3.x (modifiche API/Flusso di lavoro):{#upgrading-from-x-lazy-ad-resolving-to-lazy-ad-resolving-api-workflow-changes}

L&#39;interfaccia com.adobe.mediacore.timeline.TimelineMarker contiene ora un nuovo metodo:

**Placement.Type getPlacementType()**

Questo metodo restituirà un tipo di posizionamento di Placement.Type.PRE_ROLL, Placement.Type.MID_ROLL o Placement.Type.POST_ROLL. Se un&#39;interruzione pubblicitaria non è risolta, il metodo `getDuration()`sull&#39;interfaccia di TimelineMarker restituirà 0.

>[!NOTE]
>
>Questa interfaccia non viene sempre inserita nel tipo com.mediacore.timeline.advertising.AdBreakTimelineItem se non è ancora stata risolta. Sarà in grado di essere inserito se il metodo `getDuration()` di TimelineMarker è maggiore di 0.

**Modifiche evento:**

`kEventAdResolutionComplete` ora viene ammortizzato e ora viene attivato immediatamente dopo che il lettore entra nello stato PREPARATO. Le applicazioni che in precedenza hanno ascoltato solo questo evento per disegnare la barra di scorrimento devono modificarlo per ascoltare solo `kEventTimelineUpdated`. Dopo la risoluzione di singole interruzioni pubblicitarie, viene inviato un nuovo evento `kEventTimelineUpdated` .
