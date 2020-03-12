---
description: Queste classi forniscono informazioni sugli annunci che si verificano all'interno di una cronologia.
seo-description: Queste classi forniscono informazioni sugli annunci che si verificano all'interno di una cronologia.
seo-title: Classi pubblicitarie nella timeline
title: Classi pubblicitarie nella timeline
uuid: 4e6ca9fb-9e68-4625-a24b-386a50333862
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Classi pubblicitarie nella timeline{#timeline-advertising-classes}

Queste classi forniscono informazioni sugli annunci che si verificano all&#39;interno di una cronologia.

Pacchetto: [com.adobe.mediacore.timeline.advertising](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/package-summary.html)

Pacchetto: [com.adobe.mediacore.timeline.advertising.auditude](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/auditude/package-summary.html)

| Nome | Descrizione |
|--- |--- |
| [Annuncio](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/Ad.html) | Classe che definisce l&#39;astrazione degli annunci e contiene tutte le informazioni sugli annunci. È definito da un ID univoco, una durata e un `MediaResource`. L&#39; `MediaResource` URL contiene l&#39;URL in cui risiede il contenuto effettivo dell&#39;annuncio. |
| [AdAsset](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdAsset.html) | Classe che rappresenta una risorsa da visualizzare. Classe che rappresenta una risorsa annuncio. |
| [AdBreak](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdBreak.html) | Classe che offre una visualizzazione unificata su diversi annunci che verranno riprodotti in un determinato momento durante la riproduzione. |
| [AdBreakPlacement](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdBreakPlacement.html) | Classe dell&#39;operazione di posizionamento dell&#39;interruzione dell&#39;annuncio. |
| [AdBreakPolicy](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdBreakPolicy.html) | Enumerazione che definisce i criteri di riproduzione degli annunci correlati all&#39;utente aggirando gli annunci durante la ricerca. |
| [AdClick](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdClick.html) | Classe che rappresenta un’istanza di clic associata a una risorsa. Questa istanza contiene informazioni sull’URL di click-through e sul titolo che è possibile utilizzare per fornire ulteriori informazioni all’utente. |
| [AdPolicyInfo](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdPolicyInfo.html) | Interfaccia che definisce le proprietà per le chiamate API AdPolicySelector. Queste proprietà forniscono il contesto per l&#39;imposizione di ogni comportamento annuncio. |
| [AdPolicySelector](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdPolicySelector.html) | Un&#39;interfaccia di selezione criteri per l&#39;annuncio da applicare. Le applicazioni possono essere conformi a questa interfaccia implementando tutti i metodi richiesti o estendendo la classe di selezione dei criteri predefinita esistente per personalizzare comportamenti specifici. |
| `auditude.AuditudeAdProvider` | Obsoleto. Utilizzare AuditudeResolver. |
| [AuditudeResolver](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/auditude/AuditudeResolver.html) | Classe che gestisce la risoluzione di annunci in primetime nel processo Phrase. |
| [AuditudeTracker](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/auditude/AuditudeTracker.html) | Classe che implementa l&#39;interfaccia ContentTracker e definisce gli eventi di tracciamento annunci Primetime. |
| [ContentResolver](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/ContentResolver.html) | Classe che gestisce la parte di risoluzione degli annunci nel processo Phrase. |
| [ContentTracker](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/ContentTracker.html) | Interfaccia che definisce il protocollo da implementare se si desidera creare un modulo di tracciamento degli annunci da integrare con la libreria o con un tracciatore di annunci personalizzato. Questa interfaccia richiede la definizione del modo in cui gli eventi di avanzamento annuncio vengono segnalati al sistema di tracciamento annunci remoto. |
| [PlacementInformation](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/PlacementInformation.html) | Classe che raccoglie una richiesta di informazioni sul posizionamento. A ciascun annuncio risolto deve essere collegata una sola informazione di posizionamento. Le informazioni sulla posizione descrivono la posizione in cui l&#39;annuncio deve essere inserito nella timeline. Contiene informazioni quali: <ul><li>Posizione (in ms) </li><li>Tipo di posizionamento (preroll, medio o post-rollio) </li><li>Durata del blocco contenuto principale che sta per essere sostituito</li></ul> |
