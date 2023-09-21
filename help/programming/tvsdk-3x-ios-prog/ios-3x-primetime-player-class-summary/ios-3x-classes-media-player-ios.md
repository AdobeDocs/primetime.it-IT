---
description: Puoi utilizzare l’API Objective-C del lettore Primetime per personalizzare il comportamento del lettore.
title: Classi di lettore multimediale
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---

# Classi di lettore multimediale {#media-player-classes}

Puoi utilizzare l’API Objective-C del lettore Primetime per personalizzare il comportamento del lettore.

Queste classi descrivono il lettore multimediale e le relative risorse.

| Classe | Descrizione |
|---|---|
| PTABRControlParameters | Incapsula tutti i parametri di controllo del bit rate adattivo. I parametri supportati sono:<ul><li>minBitRate</li><li>maxBitRate</li><li>initialBitRate</li></ul> |
| PTDefaultMediaPlayerClientFactory | Implementazione predefinita di PTMediaPlayerClientFactory in TVSDK. Fornisce le istanze availablePTOpportunityResolver, PTContentResolver e PTAdPolicySelector. |
| PTMediaPlayer | Definisce il componente radice per il framework del lettore Primetime.Le applicazioni creano un&#39;istanza di questa classe per riprodurre un file multimediale. Questo componente invia notifiche per comunicare all’applicazione lo stato del lettore in qualsiasi momento. |
| PTMediaPlayerClientFactory | Protocollo che descrive i metodi che un client factory del lettore multimediale personalizzato deve implementare per fornire le istanze PTOpportunityResolver ,PTContentResolver e PTAdPolicySelector disponibili. |
| PTMediaPlayerItem | Rappresenta un supporto audio-video specifico. |
| PTMediaPlayerView | Gestisce il componente di visualizzazione del framework del lettore Primetime. |
| PTMediaProfile | Rappresenta il profilo di un singolo flusso nella playlist delle varianti. |
| PTMediaSelectionOption | Rappresenta una risorsa di media audiovisivi per adattarsi a diverse preferenze linguistiche, requisiti di accessibilità o configurazioni di applicazioni personalizzate. Tipi di opzioni validi:<ul><li>Sottotitoli (PTMediaSelectionOptionTypeSubtitle)</li><li>Audio alternativo (PTMediaSelectionOptionTypeAudio)</li><li>Sottotitoli codificati (PTMediaSelectionOptionTypeCC)</li><li>Non definito (PTMediaSelectionOptionTypeUndefined)</li></ul> |
| classe PTOpportunityResolver,protocollo PTOpportunityResolver | Classe utilizzata per l’elaborazione dei segnali nel manifesto che verranno utilizzati come posizionamenti per il processo decisionale per gli annunci di Adobe Primetime. |
| PTOpportunityResolverDelegate | Protocollo che descrive i metodi che il risolutore opportunità personalizzato ( PTOpportunityResolver ) deve utilizzare per comunicare al delegato lo stato della risoluzione dell&#39;opportunità. |
| PTSDK | Descrive la versione di TVSDK e le relative funzionalità. |
| PTSDKConfig | Espone le impostazioni globali di TVSDK e consente a un’applicazione di abbonarsi a tag HLS personalizzati. |
| PTTextStyleRule | Definisce le costanti che rappresentano le chiavi di attributo di stile del testo che costituiscono il dizionario delle regole. |
