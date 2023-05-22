---
description: L'oggetto DRMAuthenticateEvent viene inviato quando un oggetto Primetime tenta di riprodurre contenuto protetto che richiede credenziali utente per l'autenticazione prima della riproduzione (e l'autenticazione non è ancora stata eseguita). Il gestore DRMAuthenticateEvent è responsabile della raccolta delle credenziali richieste (nome utente, password e tipo) e del passaggio dei valori al metodo .setDRMAuthenticationCredentials() per la convalida.
title: Creare un gestore DRMAuthenticateEvent
exl-id: fe01340b-8a76-4fd4-8c6c-85454d0e2218
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---

# Creare un gestore DRMAuthenticateEvent{#create-a-drmauthenticateevent-handler}

L&#39;oggetto DRMAuthenticateEvent viene inviato quando un oggetto Primetime tenta di riprodurre contenuto protetto che richiede credenziali utente per l&#39;autenticazione prima della riproduzione (e l&#39;autenticazione non è ancora stata eseguita). Il gestore DRMAuthenticateEvent è responsabile della raccolta delle credenziali richieste (nome utente, password e tipo) e del passaggio dei valori al metodo .setDRMAuthenticationCredentials() per la convalida.

L’applicazione deve fornire un meccanismo per ottenere le credenziali utente. Ad esempio, l’applicazione potrebbe fornire a un utente una semplice interfaccia utente per immettere i valori del nome utente e della password. Inoltre, deve fornire un meccanismo per gestire e limitare i tentativi di autenticazione non riusciti ripetuti.

Creare un gestore eventi che trasmette un set di credenziali di autenticazione hardcoded all&#39;oggetto Primetime che ha generato l&#39;evento:

```
var connection:NetConnection = new NetConnection();  
connection.connect(null);  
var videoStream:Primetime = new Primetime(connection);  
 
videoStream.addEventListener( 
  DRMAuthenticateEvent.DRM_AUTHENTICATE,  
  drmAuthenticateEventHandler)  
  private function drmAuthenticateEventHandler(event:DRMAuthenticateEvent):void {  
    videoStream.setDRMAuthenticationCredentials("administrator", "password", "drm");  
} 
```

(Il codice per la riproduzione del video e per verificare che sia stata stabilita una connessione al flusso video non è incluso in questa sezione.)
