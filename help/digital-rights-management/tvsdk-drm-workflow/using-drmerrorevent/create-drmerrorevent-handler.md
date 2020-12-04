---
seo-title: Creare un gestore DRMErrorEvent
title: Creare un gestore DRMErrorEvent
uuid: dde660fc-6899-47d4-97d4-46acda2db262
translation-type: tm+mt
source-git-commit: 5749142d42f7d7b36c96592955d1f71f6a7956fc
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 0%

---


# Creare un gestore DRMErrorEvent{#create-a-drmerrorevent-handler}

Creare un gestore eventi per elaborare gli eventi di errore inviati da Primetime quando si verifica un errore durante il tentativo di riprodurre il contenuto protetto.

Normalmente, quando un&#39;applicazione rileva un errore, esegue un numero qualsiasi di attività di pulizia. Quindi, informa l&#39;utente dell&#39;errore e fornisce le opzioni per risolvere il problema.

```
private function drmErrorEventHandler(event:DRMErrorEvent):void {  
    trace(event.toString());  
} 
```

