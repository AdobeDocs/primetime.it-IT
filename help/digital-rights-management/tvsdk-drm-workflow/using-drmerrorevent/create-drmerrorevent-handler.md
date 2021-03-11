---
title: Creare un gestore DRMErrorEvent
description: Creare un gestore DRMErrorEvent
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 0%

---


# Crea un gestore DRMErrorEvent{#create-a-drmerrorevent-handler}

Crea un gestore di eventi per elaborare gli eventi di errore inviati da Primetime quando viene rilevato un errore durante il tentativo di riprodurre contenuto protetto.

Normalmente, quando un&#39;applicazione rileva un errore, esegue un numero qualsiasi di attività di pulizia. Quindi informa l&#39;utente dell&#39;errore e fornisce le opzioni per risolvere il problema.

```
private function drmErrorEventHandler(event:DRMErrorEvent):void {  
    trace(event.toString());  
} 
```

