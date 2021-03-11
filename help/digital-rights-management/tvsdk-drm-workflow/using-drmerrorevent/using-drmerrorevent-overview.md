---
title: Panoramica sull'utilizzo della classe DRMErrorEvent
description: Panoramica sull'utilizzo della classe DRMErrorEvent
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---


# Panoramica della classe DRMErrorEvent {#using-the-drmerrorevent-class-overview}

Primetime invia un oggetto `DRMErrorEvent` quando un oggetto Primetime, che tenta di riprodurre contenuto protetto, incontra un [errore relativo a DRM](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages). Se le credenziali utente non sono valide, l&#39;oggetto `DRMAuthenticateEvent` invia ripetutamente fino a quando l&#39;utente non immette credenziali valide o l&#39;applicazione nega ulteriori tentativi. L&#39;applicazione è responsabile dell&#39;ascolto di qualsiasi altro evento di errore DRM per rilevare, identificare e gestire gli [errori relativi a DRM](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages).

Anche con credenziali utente valide, i termini della licenza del contenuto possono comunque impedire a un utente di visualizzare il contenuto crittografato. Ad esempio, a un utente può essere negato l’accesso per il tentativo di visualizzare il contenuto in un’applicazione non autorizzata (ad esempio, Elenco Consentiti applicazione). Un’applicazione non autorizzata è un’applicazione che non è stata firmata con un certificato di firma dell’applicazione inserito nell’elenco Consentiti. In questo caso, viene inviato un oggetto `DRMErrorEvent` .

Gli eventi di errore possono anche essere attivati se il contenuto è danneggiato o se la versione dell’applicazione non corrisponde a quanto specificato dalla licenza. L&#39;applicazione deve fornire un meccanismo adeguato per la gestione degli errori.
