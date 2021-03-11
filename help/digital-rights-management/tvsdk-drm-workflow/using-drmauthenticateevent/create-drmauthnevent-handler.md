---
description: L'oggetto DRMAuthenticateEvent viene inviato quando un oggetto Primetime tenta di riprodurre contenuto protetto che richiede una credenziale utente per l'autenticazione prima della riproduzione (e l'autenticazione non è ancora stata eseguita). Il gestore DRMAuthenticateEvent è responsabile della raccolta delle credenziali richieste (nome utente, password e tipo) e del passaggio dei valori al metodo .setDRMAuthAuthenticationCredentials() per la convalida.
title: Creare un gestore DRMAuthenticateEvent
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# Crea un gestore DRMAuthenticateEvent{#create-a-drmauthenticateevent-handler}

L&#39;oggetto DRMAuthenticateEvent viene inviato quando un oggetto Primetime tenta di riprodurre contenuto protetto che richiede una credenziale utente per l&#39;autenticazione prima della riproduzione (e l&#39;autenticazione non è ancora stata eseguita). Il gestore DRMAuthenticateEvent è responsabile della raccolta delle credenziali richieste (nome utente, password e tipo) e del passaggio dei valori al metodo .setDRMAuthAuthenticationCredentials() per la convalida.

L&#39;applicazione deve fornire un meccanismo per ottenere le credenziali utente. Ad esempio, l&#39;applicazione potrebbe fornire a un utente una semplice interfaccia utente per immettere i valori di nome utente e password. Inoltre, dovrebbe fornire un meccanismo per gestire e limitare i ripetuti tentativi di errore di autenticazione.

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

(Il codice per la riproduzione del video e per verificare che sia stata effettuata una connessione corretta allo streaming video non è incluso qui.)
