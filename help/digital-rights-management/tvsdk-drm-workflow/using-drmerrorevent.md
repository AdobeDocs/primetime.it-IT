---
title: Utilizzo della panoramica della classe DRMErrorEvent
description: Utilizzo della panoramica della classe DRMErrorEvent
copied-description: true
exl-id: c651cdcf-f8f8-4085-a88e-d82030f90f11
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---

# Utilizzo della classe DRMErrorEvent {#using-the-drmerrorevent-class}

Primetime invia una `DRMErrorEvent` oggetto quando un oggetto Primetime, che tenta di riprodurre contenuto protetto, incontra un [Errore relativo a DRM](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages). Se le credenziali utente non sono valide, `DRMAuthenticateEvent` L&#39;oggetto viene inviato ripetutamente fino a quando l&#39;utente immette credenziali valide o l&#39;applicazione nega ulteriori tentativi. L&#39;applicazione è responsabile dell&#39;ascolto di qualsiasi altro evento di errore DRM per rilevare, identificare e gestire [Errori relativi al DRM](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages).

Anche con credenziali utente valide, i termini della licenza del contenuto possono ancora impedire a un utente di visualizzare il contenuto crittografato. Ad esempio, a un utente può essere negato l’accesso per il tentativo di visualizzare il contenuto in un’applicazione non autorizzata (ad esempio, Inserimento nell’elenco Consentiti dall’applicazione). Un’applicazione non autorizzata è un’applicazione che non è stata firmata con un certificato di firma dell’applicazione inserito nell’elenco Consentiti. In questo caso, un `DRMErrorEvent` l&#39;oggetto viene inviato.

Gli eventi di errore possono essere attivati anche se il contenuto è danneggiato o se la versione dell’applicazione non corrisponde a quanto specificato dalla licenza. La domanda deve fornire un meccanismo adeguato per la gestione degli errori.

## Creare un gestore DRMErrorEvent {#create-a-drmerrorevent-handler}

Crea un gestore eventi per elaborare gli eventi di errore inviati da Primetime quando si verifica un errore durante il tentativo di riproduzione di contenuto protetto.

In genere, quando un&#39;applicazione rileva un errore, esegue un numero qualsiasi di attività di pulizia. Quindi informa l’utente dell’errore e fornisce le opzioni per risolvere il problema.

```
private function drmErrorEventHandler(event:DRMErrorEvent):void {  
    trace(event.toString());  
} 
```
