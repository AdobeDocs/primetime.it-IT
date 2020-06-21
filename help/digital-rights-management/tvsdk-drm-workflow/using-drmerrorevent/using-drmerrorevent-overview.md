---
seo-title: Utilizzo della panoramica della classe DRMErrorEvent
title: Utilizzo della panoramica della classe DRMErrorEvent
uuid: cbb9c1a7-3c50-479d-b7e5-63010a696dfa
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---


# Utilizzo della panoramica della classe DRMErrorEvent {#using-the-drmerrorevent-class-overview}

Primetime invia un `DRMErrorEvent` oggetto quando un oggetto Primetime, che tenta di riprodurre contenuto protetto, restituisce un errore [relativo a](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages)DRM. Se le credenziali utente non sono valide, l&#39; `DRMAuthenticateEvent` oggetto viene inviato ripetutamente fino a quando l&#39;utente non immette credenziali valide o l&#39;applicazione non nega ulteriori tentativi. L&#39;applicazione è responsabile dell&#39;ascolto di qualsiasi altro evento di errore DRM per rilevare, identificare e gestire gli errori [relativi a](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages)DRM.

Anche con credenziali utente valide, i termini della licenza del contenuto possono comunque impedire a un utente di visualizzare il contenuto crittografato. Ad esempio, a un utente può essere negato l&#39;accesso per aver tentato di visualizzare il contenuto in un&#39;applicazione non autorizzata (ad esempio, elenco Consentito applicazione). Un&#39;applicazione non autorizzata è un&#39;applicazione che non è stata firmata con un certificato di firma delle applicazioni incluso nell&#39;elenco di autorizzazione. In questo caso, viene inviato un `DRMErrorEvent` oggetto.

Gli eventi di errore possono essere attivati anche se il contenuto è danneggiato o se la versione dell&#39;applicazione non corrisponde a quanto specificato dalla licenza. L&#39;applicazione deve fornire un meccanismo appropriato per la gestione degli errori.
