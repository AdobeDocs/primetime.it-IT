---
description: Queste classi forniscono informazioni sugli annunci che si verificano in una timeline.
title: Classi di pubblicità Timeline
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 0%

---

# Classi di pubblicità Timeline{#timeline-advertising-classes}

Queste classi forniscono informazioni sugli annunci che si verificano in una timeline.

Pacchetto [com.adobe.mediacore.timeline.advertising](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/package-summary.html)

Pacchetto [com.adobe.mediacore.timeline.advertising.auditude](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/auditude/package-summary.html)

| Nome | Descrizione |
|--- |--- |
| [Annuncio](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/Ad.html) | Classe che definisce l’astrazione dell’annuncio e contiene tutte le informazioni sull’annuncio. È definito da un ID univoco, una durata e un `MediaResource`. Il `MediaResource` contiene l’URL in cui risiede il contenuto dell’annuncio effettivo. |
| [AdAsset](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdAsset.html) | Classe che rappresenta una risorsa da visualizzare. Classe che rappresenta una risorsa annuncio. |
| [AdBreak](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdBreak.html) | Classe che offre una visualizzazione unificata su diversi annunci che verranno riprodotti ad un certo punto durante la riproduzione. |
| [AdBreakPlacement](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdBreakPlacement.html) | Classe dell’operazione di posizionamento dell’interruzione pubblicitaria. |
| [AdBreakPolicy](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdBreakPolicy.html) | Enumerazione che definisce il criterio di riproduzione dell’annuncio relativo all’utente ignorando gli annunci durante la ricerca. |
| [AdClick](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdClick.html) | Classe che rappresenta un’istanza di clic associata a una risorsa. Questa istanza contiene informazioni sull’URL di click-through e il titolo che può essere utilizzato per fornire ulteriori informazioni all’utente. |
| [AdPolicyInfo](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdPolicyInfo.html) | Interfaccia che definisce le proprietà per le chiamate API AdPolicySelector. Queste proprietà forniscono il contesto per applicare ogni comportamento pubblicitario. |
| [AdPolicySelector](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdPolicySelector.html) | Un’interfaccia del selettore dei criteri degli annunci per applicare i comportamenti degli annunci. Le applicazioni possono conformarsi a questa interfaccia implementando tutti i metodi richiesti o estendendo la classe del selettore dei criteri predefinita esistente per personalizzare comportamenti specifici. |
| `auditude.AuditudeAdProvider` | Obsoleto. Utilizza AuditudeResolver. |
| [AuditudeResolver](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/auditude/AuditudeResolver.html) | Classe che gestisce la prima e la risoluzione nel processo della frase. |
| [AuditudeTracker](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/auditude/AuditudeTracker.html) | Classe che implementa l&#39;interfaccia ContentTracker e definisce gli eventi di tracciamento degli annunci Primetime. |
| [ContentResolution](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/ContentResolver.html) | Classe che gestisce la parte di risoluzione degli annunci nel processo della frase. |
| [ContentTracker](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/ContentTracker.html) | Interfaccia che definisce il protocollo da implementare per creare un modulo di ad-tracking progettato per l’integrazione con la libreria o un ad tracker personalizzato. Questa interfaccia richiede la definizione del modo in cui gli eventi di avanzamento degli annunci vengono segnalati al sistema remoto di tracciamento degli annunci. |
| [Informazioni sul posizionamento](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/PlacementInformation.html) | Classe che astrae una richiesta di informazioni sul posizionamento. A ogni annuncio risolto devono essere associate una informazione di posizionamento. Le informazioni sul posizionamento descrivono dove l’annuncio deve essere inserito nella timeline. Contiene informazioni quali: <ul><li>Posizione posizionamento (in ms) </li><li>Tipo di posizionamento (pre-roll, mid-roll o post-roll) </li><li>Durata del blocco di contenuto principale che sta per essere sostituito</li></ul> |
