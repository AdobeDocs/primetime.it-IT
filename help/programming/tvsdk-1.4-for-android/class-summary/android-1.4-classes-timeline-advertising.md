---
description: Queste classi forniscono informazioni sugli annunci che si verificano all'interno di una timeline.
title: Classi pubblicitarie Timeline
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 0%

---


# Classi pubblicitarie Timeline{#timeline-advertising-classes}

Queste classi forniscono informazioni sugli annunci che si verificano all&#39;interno di una timeline.

Pacchetto: [com.adobe.mediacore.timeline.advertising](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/package-summary.html)

Pacchetto: [com.adobe.mediacore.timeline.advertising.auditude](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/auditude/package-summary.html)

| Nome | Descrizione |
|--- |--- |
| [Annuncio](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/Ad.html) | Classe che definisce l’astrazione dell’annuncio e contiene tutte le informazioni sull’annuncio. È definito da un ID univoco, una durata e un `MediaResource`. Il `MediaResource` contiene l&#39;URL in cui si trova il contenuto effettivo dell&#39;annuncio. |
| [AdAsset](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdAsset.html) | Classe che rappresenta una risorsa da visualizzare. Classe che rappresenta una risorsa pubblicitaria. |
| [AdBreak](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdBreak.html) | Classe che offre una visualizzazione unificata su diversi annunci che verranno riprodotti ad un certo punto durante la riproduzione. |
| [AdBreakPlacement](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdBreakPlacement.html) | Classe di operazione di posizionamento dell’interruzione dell’annuncio. |
| [AdBreakPolicy](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdBreakPolicy.html) | Enumerazione che definisce i criteri di riproduzione degli annunci relativi all’utente bypassando gli annunci durante la ricerca. |
| [AdClick](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdClick.html) | Classe che rappresenta un’istanza di clic associata a una risorsa. Questa istanza contiene informazioni sull’URL di click-through e sul titolo che possono essere utilizzati per fornire informazioni aggiuntive all’utente. |
| [AdPolicyInfo](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdPolicyInfo.html) | Interfaccia che definisce le proprietà per le chiamate API AdPolicySelector. Queste proprietà forniscono il contesto per applicare ogni comportamento pubblicitario. |
| [AdPolicySelector](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdPolicySelector.html) | Interfaccia di selezione dei criteri per l’applicazione dei comportamenti degli annunci. Le applicazioni possono conformarsi a questa interfaccia implementando tutti i metodi richiesti o estendendo la classe di selettore dei criteri predefinita esistente per personalizzare comportamenti specifici. |
| `auditude.AuditudeAdProvider` | Obsoleto. Utilizza AuditudeResolver. |
| [AuditudeResolver](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/auditude/AuditudeResolver.html) | Classe che gestisce la risoluzione di annunci in primetime nel processo della frase. |
| [AuditudeTracker](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/auditude/AuditudeTracker.html) | Classe che implementa l&#39;interfaccia ContentTracker e definisce gli eventi di tracciamento degli annunci Primetime. |
| [ContentResolver](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/ContentResolver.html) | Classe che gestisce la parte di risoluzione degli annunci nel processo di Frase. |
| [ContentTracker](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/ContentTracker.html) | Interfaccia che definisce il protocollo da implementare se desideri creare un modulo di tracciamento degli annunci progettato per l&#39;integrazione con la libreria o un tracciamento degli annunci personalizzato. Questa interfaccia richiede di definire il modo in cui gli eventi di avanzamento degli annunci vengono segnalati al sistema di tracciamento degli annunci remoti. |
| [InformazioniPosizionamento](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/PlacementInformation.html) | Classe che astratta una richiesta di informazioni sul posizionamento. A ogni annuncio risolto deve essere collegata una sola informazione di posizionamento. Le informazioni sul posizionamento descrivono dove l’annuncio deve essere inserito nella timeline. Contiene informazioni quali: <ul><li>Posizione (in ms) </li><li>Tipo di posizionamento (pre-roll, mid-roll o post-roll) </li><li>Durata del blocco di contenuto principale che sta per essere sostituito</li></ul> |
