---
description: È possibile utilizzare l'API Objective-C di Lettore Primetime per personalizzare il comportamento del lettore.
seo-description: È possibile utilizzare l'API Objective-C di Lettore Primetime per personalizzare il comportamento del lettore.
seo-title: Lezioni di Media Player
title: Lezioni di Media Player
uuid: 705c71b6-4e5e-46b5-a59d-13df977b04f2
translation-type: tm+mt
source-git-commit: b13f2d3f083a6ca333a4edba1c8d7261f7d448ad
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---


# Classi di lettori multimediali {#media-player-classes}

È possibile utilizzare l&#39;API Objective-C di Lettore Primetime per personalizzare il comportamento del lettore.

Queste classi descrivono il lettore multimediale e le relative risorse.

| Classe | Descrizione |
|---|---|
| PTABRControlParameters | Incapsula tutti i parametri di controllo bitrate adattivi. I parametri supportati sono:<ul><li>minBitRate</li><li>maxBitRate</li><li>initialBitRate</li></ul> |
| PTDefaultMediaPlayerClientFactory | Implementazione predefinita di PTMediaPlayerClientFactoryin TVSDK. Fornisce le istanze disponibiliPTOpportunityResolver, PTContentResolver e PTAdPolicySelector. |
| PTMediaPlayer | Definisce il componente principale per il framework di Primetime Player.Le applicazioni creano un&#39;istanza di questa classe per riprodurre un supporto. Questo componente invia notifiche per informare l’applicazione dello stato del lettore in un dato momento. |
| PTMediaPlayerClientFactory | Protocollo che descrive i metodi che un client client client Media Player personalizzato deve implementare per fornire le istanze PTOpportunityResolver, PTCContentResolver e PTAdPolicySelector disponibili. |
| PTMediaPlayerItem | Rappresenta un supporto audio-video specifico. |
| PTMediaPlayerView | Gestisce il componente di visualizzazione del framework Primetime Player. |
| PTMediaProfile | Rappresenta il profilo di un singolo flusso nella playlist della variante. |
| PTMediaSelectionOption | Rappresenta una risorsa multimediale audiovisiva in grado di soddisfare diverse preferenze linguistiche, requisiti di accessibilità o configurazioni di applicazioni personalizzate. Tipi di opzioni validi:<ul><li>Sottotitoli (PTMediaSelectionOptionTypeSubtitle)</li><li>Audio alternativo (PTMediaSelectionOptionTypeAudio)</li><li>Sottotitoli codificati (PTMediaSelectionOptionTypeCC)</li><li>Non definito (PTMediaSelectionOptionTypeUndefined)</li></ul> |
| PTOpportunityResolver, classe PTOpportunityResolver, protocollo | Classe utilizzata per l&#39;elaborazione di segnali in-manifest che verranno utilizzati come punti di posizionamento per il processo di decisione  Adobe Primetime. |
| PTOpportunityResolverDelegate | Protocollo che descrive i metodi che il risolutore di opportunità personalizzato ( PTOpportunityResolver ) dovrebbe utilizzare per comunicare al delegato lo stato della risoluzione dell&#39;opportunità. |
| PTSDK | Descrive la versione di TVSDK e le sue funzionalità. |
| PTSDKConfig | Espone le impostazioni globali TVSDK e consente a un&#39;applicazione di sottoscrivere tag HLS personalizzati. |
| PTTextStyleRule | Definisce costanti che rappresentano le chiavi degli attributi di stile di testo che formano il dizionario delle regole. |
