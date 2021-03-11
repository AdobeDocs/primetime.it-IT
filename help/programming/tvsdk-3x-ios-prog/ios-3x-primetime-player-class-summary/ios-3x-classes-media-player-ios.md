---
description: Puoi utilizzare l'API Objective-C di Primetime Player per personalizzare il comportamento del lettore.
title: Classi di lettori multimediali
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---


# Classi di lettori multimediali {#media-player-classes}

Puoi utilizzare l&#39;API Objective-C di Primetime Player per personalizzare il comportamento del lettore.

Queste classi descrivono il lettore multimediale e le relative risorse.

| Classe | Descrizione |
|---|---|
| PTABRControlParameters | Racchiude tutti i parametri di controllo del bit rate adattivo. I parametri supportati sono:<ul><li>minBitRate</li><li>maxBitRate</li><li>initialBitRate</li></ul> |
| PTDefaultMediaPlayerClientFactory | Implementazione predefinita di PTMediaPlayerClientFactoryin TVSDK. Fornisce le istanze availablePTOpportunityResolver, PTContentResolver e PTAdPolicySelector. |
| PTMediaPlayer | Definisce il componente principale per il framework di Primetime Player.Le applicazioni creano un&#39;istanza di questa classe per riprodurre un contenuto multimediale. Questo componente invia notifiche per comunicare all’applicazione lo stato del lettore in un dato momento. |
| PTMediaPlayerClientFactory | Protocollo che descrive i metodi che un client factory del lettore multimediale personalizzato deve implementare per fornire le istanze PTOpportunityResolver, PTContentResolver e PTAdPolicySelector disponibili. |
| PTMediaPlayerItem | Rappresenta un supporto audio-video specifico. |
| PTMediaPlayerView | Gestisce il componente di visualizzazione del framework di Primetime Player. |
| PTMediaProfile | Rappresenta il profilo di un singolo flusso nella playlist della variante. |
| PTMediaSelectionOption | Rappresenta una risorsa multimediale audiovisiva per soddisfare diverse preferenze linguistiche, requisiti di accessibilità o configurazioni di applicazioni personalizzate. Tipi di opzioni validi:<ul><li>Sottotitoli (PTMediaSelectionOptionTypeSubtitle)</li><li>Audio alternativo (PTMediaSelectionOptionTypeAudio)</li><li>Sottotitoli codificati (PTMediaSelectionOptionTypeCC)</li><li>Non definito (PTMediaSelectionOptionTypeUndefined)</li></ul> |
| PTOpportunityResolver, protocollo PTOpportunityResolver | Classe utilizzata per l&#39;elaborazione di segnali in-manifest che verranno utilizzati come posizionamenti per il processo di ad decision ioning di Adobe Primetime. |
| PTOpportunityResolverDelegate | Protocollo che descrive i metodi che il risolutore di opportunità personalizzato ( PTOpportunityResolver ) deve utilizzare per comunicare al delegato lo stato della risoluzione dell&#39;opportunità. |
| PTSDK | Descrive la versione del TVSDK e le sue funzionalità. |
| PTSDKConfig | Espone le impostazioni globali TVSDK e consente a un&#39;applicazione di abbonarsi ai tag HLS personalizzati. |
| RegolaStileTesto | Definisce costanti che rappresentano le chiavi dell&#39;attributo di stile del testo che formano il dizionario delle regole. |
