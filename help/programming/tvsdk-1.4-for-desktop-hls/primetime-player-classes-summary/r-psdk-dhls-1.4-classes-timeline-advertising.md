---
description: Queste classi forniscono informazioni sugli annunci che si verificano all'interno di una timeline.
title: Classi pubblicitarie Timeline
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 0%

---


# Classi pubblicitarie Timeline {#timeline-advertising-classes}

Queste classi forniscono informazioni sugli annunci che si verificano all&#39;interno di una timeline.

Pacchetto: [com.adobe.mediacore.timeline.advertising](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/package-detail.html)
Pacchetto: [com.adobe.mediacore.timeline.advertising.policy](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/package-detail.html)

| Nome | Descrizione |
|---|---|
| [Annuncio](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/Ad.html) | Classe che definisce l’astrazione dell’annuncio e contiene tutte le informazioni sull’annuncio. È definito da un ID univoco, una durata e un `MediaResource`. Il `MediaResource` contiene l&#39;URL in cui si trova il contenuto effettivo dell&#39;annuncio. |
| [AdAsset](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdAsset.html) | Classe che rappresenta una risorsa da visualizzare. Classe che rappresenta una risorsa pubblicitaria. |
| [AdBreak](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdBreak.html) | Classe che offre una visualizzazione unificata su diversi annunci che verranno riprodotti ad un certo punto durante la riproduzione. |
| [AdBreakPolicy](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdBreakPolicy.html) | Enumerazione che definisce i criteri di riproduzione degli annunci relativi all’utente bypassando gli annunci durante la ricerca. |
| [AdBreakTimelineItem](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdBreakTimelineItem.html) | Elemento Timeline associato all’interruzione annuncio specifica. |
| [AdBreakWatchedPolicy](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdBreakWatchedPolicy.html) | Classe di enumerazione per i possibili criteri su quando contrassegnare un&#39;interruzione pubblicitaria come osservata. |
| [AdClick](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdClick.html) | Classe che rappresenta un’istanza di clic associata a una risorsa. Questa istanza contiene informazioni sull’URL di click-through e sul titolo che possono essere utilizzati per fornire informazioni aggiuntive all’utente. |
| [AdPolicy](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicy.html) | Classe di enumerazione per i possibili criteri su dove riprendere a riprodurre un annuncio dopo la ricerca o la modalità di gioco-trucco. |
| [AdPolicyMode](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicyMode.html) | Classe di enumerazione che elenca i modi in cui il lettore sta riproducendo, ad esempio ricerca o riproduzione normale. |
| [AdPolicyInfo](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicySelector.html) | Interfaccia che definisce le proprietà per le chiamate API `AdPolicySelector`. Queste proprietà forniscono il contesto per applicare ogni comportamento pubblicitario. |
| [AdPolicySelector](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicySelector.html) | Interfaccia di selezione dei criteri per l’applicazione dei comportamenti degli annunci. Le applicazioni possono conformarsi a questa interfaccia implementando tutti i metodi richiesti o estendendo la classe di selettore dei criteri predefinita esistente per personalizzare comportamenti specifici. |
| [AdTimelineItem](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdTimelineItem.html) | Elemento Timeline associato a un annuncio specifico. |
| [AuditudeAdResolver](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AuditudeAdResolver.html) | Classe che gestisce la risoluzione di annunci in primetime nel processo TVSDK. |
| [AdType](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdType.html) | Enumerazione di tutti i tipi di annunci supportati da TVSDK. |
| [MetadataAdResolver](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/MetadataAdResolver.html) | Classe. |

