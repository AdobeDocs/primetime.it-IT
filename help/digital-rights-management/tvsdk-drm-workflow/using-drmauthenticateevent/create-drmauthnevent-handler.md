---
description: L'oggetto DRMAuthenticateEvent viene inviato quando un oggetto Primetime tenta di riprodurre contenuto protetto che richiede una credenziale utente per l'autenticazione prima della riproduzione (e l'autenticazione non è ancora stata eseguita). Il gestore DRMAuthenticateEvent è responsabile della raccolta delle credenziali richieste (nome utente, password e tipo) e del passaggio dei valori al metodo .setDRMAuthenticationCredentials() per la convalida.
seo-description: L'oggetto DRMAuthenticateEvent viene inviato quando un oggetto Primetime tenta di riprodurre contenuto protetto che richiede una credenziale utente per l'autenticazione prima della riproduzione (e l'autenticazione non è ancora stata eseguita). Il gestore DRMAuthenticateEvent è responsabile della raccolta delle credenziali richieste (nome utente, password e tipo) e del passaggio dei valori al metodo .setDRMAuthenticationCredentials() per la convalida.
seo-title: Creare un gestore DRMAuthenticateEvent
title: Creare un gestore DRMAuthenticateEvent
uuid: 58330691-d0b5-46bd-9b1d-8dc597580d31
translation-type: tm+mt
source-git-commit: 5749142d42f7d7b36c96592955d1f71f6a7956fc

---


# Creare un gestore DRMAuthenticateEvent{#create-a-drmauthenticateevent-handler}

L&#39;oggetto DRMAuthenticateEvent viene inviato quando un oggetto Primetime tenta di riprodurre contenuto protetto che richiede una credenziale utente per l&#39;autenticazione prima della riproduzione (e l&#39;autenticazione non è ancora stata eseguita). Il gestore DRMAuthenticateEvent è responsabile della raccolta delle credenziali richieste (nome utente, password e tipo) e del passaggio dei valori al metodo .setDRMAuthenticationCredentials() per la convalida.

L&#39;applicazione deve fornire alcuni meccanismi per ottenere le credenziali utente. Ad esempio, l&#39;applicazione potrebbe fornire a un utente una semplice interfaccia utente per immettere i valori di nome utente e password. Inoltre, dovrebbe fornire un meccanismo per gestire e limitare i tentativi ripetuti di errore di autenticazione.

Creare un gestore di eventi che passi un set di credenziali di autenticazione hardcoded all&#39;oggetto Primetime che ha originato l&#39;evento:

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

(Il codice per riprodurre il video e verificare che sia stata stabilita una connessione corretta allo streaming video non è incluso in questo campo.)
