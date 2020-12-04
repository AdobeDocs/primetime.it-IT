---
seo-title: Creare un gestore DRMStatusEvent
title: Creare un gestore DRMStatusEvent
uuid: 64f539d9-344c-4372-88b8-c8d098af9dd8
translation-type: tm+mt
source-git-commit: 5749142d42f7d7b36c96592955d1f71f6a7956fc
workflow-type: tm+mt
source-wordcount: '47'
ht-degree: 0%

---


# Creare un gestore DRMStatusEvent{#create-a-drmstatusevent-handler}

Nell&#39;esempio seguente viene creato un gestore eventi che genera le informazioni sullo stato del contenuto DRM per l&#39;oggetto Primetime che ha originato l&#39;evento.

Aggiungete un gestore eventi a un oggetto Primetime che punta al contenuto protetto:

```
function drmStatusEventHandler(event:DRMStatusEvent):void { trace(event); } 
```

