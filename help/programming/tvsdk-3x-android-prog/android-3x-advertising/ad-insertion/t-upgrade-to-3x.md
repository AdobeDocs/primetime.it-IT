---
description: L’interfaccia com.adobe.mediacore.timeline.TimelineMarker contiene ora un nuovo metodo
title: Aggiornamento da 2.5.x Lazy Ad Resolving a 3.0.0 Lazy Ad Resolving (Modifiche API/flusso di lavoro)
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---

# Aggiornamento da 2.5.x Lazy Ad Resolving a 3.x Lazy Ad Resolving (Modifiche API/flusso di lavoro):{#upgrading-from-x-lazy-ad-resolving-to-lazy-ad-resolving-api-workflow-changes}

L’interfaccia com.adobe.mediacore.timeline.TimelineMarker contiene ora un nuovo metodo:

**Placement.Type getPlacementType()**

Questo metodo restituirà un tipo di posizionamento Placement.Type.PRE_ROLL, Placement.Type.MID_ROLL o Placement.Type.POST_ROLL. Se un’interruzione pubblicitaria non è stata risolta, il `getDuration()`sull&#39;interfaccia TimelineMarker restituirà 0.

>[!NOTE]
>
>Questa interfaccia non sempre esegue il cast nel tipo com.mediacore.timeline.advertising.AdBreakTimelineItem, se non è ancora stata risolta. Sarà possibile eseguirne il cast se `getDuration()` il valore del metodo TimelineMarker è maggiore di 0.

**Modifiche evento:**

`kEventAdResolutionComplete` ora è ammortizzato e viene attivato immediatamente dopo che il lettore entra nello stato PREPARATO. Le applicazioni che in precedenza hanno ascoltato solo questo evento per disegnare la barra di scorrimento devono modificarlo per fare in modo che ascolti `kEventTimelineUpdated` solo. Una volta risolte le singole interruzioni pubblicitarie, viene `kEventTimelineUpdated` l&#39;evento verrà inviato.
