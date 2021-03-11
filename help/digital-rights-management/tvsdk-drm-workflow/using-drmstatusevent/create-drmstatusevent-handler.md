---
title: Creare un gestore DRMStatusEvent
description: Creare un gestore DRMStatusEvent
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '47'
ht-degree: 0%

---


# Crea un gestore DRMStatusEvent{#create-a-drmstatusevent-handler}

Nell&#39;esempio seguente viene creato un gestore eventi che restituisce le informazioni sullo stato del contenuto DRM per l&#39;oggetto Primetime che ha generato l&#39;evento.

Aggiungere un gestore eventi a un oggetto Primetime che punta al contenuto protetto:

```
function drmStatusEventHandler(event:DRMStatusEvent):void { trace(event); } 
```

