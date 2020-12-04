---
description: Queste classi forniscono informazioni sugli annunci che si verificano all'interno di una cronologia.
seo-description: Queste classi forniscono informazioni sugli annunci che si verificano all'interno di una cronologia.
seo-title: Classi pubblicitarie nella timeline
title: Classi pubblicitarie nella timeline
uuid: f424fa13-778b-458d-bc82-389441a8a56a
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 0%

---


# Classi pubblicitarie della cronologia {#timeline-advertising-classes}

Queste classi forniscono informazioni sugli annunci che si verificano all&#39;interno di una cronologia.

Pacchetto: [com.adobe.mediacore.timeline.advertising](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/package-detail.html)
Pacchetto: [com.adobe.mediacore.timeline.advertising.policy](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/package-detail.html)

| Nome | Descrizione |
|---|---|
| [Annuncio](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/Ad.html) | Classe che definisce l&#39;astrazione degli annunci e contiene tutte le informazioni sugli annunci. È definito da un ID univoco, una durata e un `MediaResource`. L&#39; `MediaResource` contiene l&#39;URL in cui risiede il contenuto effettivo dell&#39;annuncio. |
| [AdAsset](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdAsset.html) | Classe che rappresenta una risorsa da visualizzare. Classe che rappresenta una risorsa annuncio. |
| [AdBreak](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdBreak.html) | Classe che offre una visualizzazione unificata su diversi annunci che verranno riprodotti in un determinato momento durante la riproduzione. |
| [AdBreakPolicy](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdBreakPolicy.html) | Enumerazione che definisce i criteri di riproduzione degli annunci correlati all&#39;utente aggirando gli annunci durante la ricerca. |
| [AdBreakTimelineItem](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdBreakTimelineItem.html) | Elemento della timeline associato all’interruzione annuncio specifica. |
| [AdBreakWatchedPolicy](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdBreakWatchedPolicy.html) | Classe di enumerazione per possibili criteri su quando contrassegnare un&#39;interruzione annuncio come osservata. |
| [AdClick](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdClick.html) | Classe che rappresenta un’istanza di clic associata a una risorsa. Questa istanza contiene informazioni sull’URL di click-through e sul titolo che è possibile utilizzare per fornire ulteriori informazioni all’utente. |
| [AdPolicy](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicy.html) | Classe di enumerazione per i possibili criteri per la ripresa della riproduzione di un&#39;interruzione annuncio dopo la ricerca o la modalità di riproduzione trucco. |
| [AdPolicyMode](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicyMode.html) | Classe di enumerazione che elenca i modi in cui il lettore viene riprodotto, ad esempio ricerca o riproduzione normale. |
| [AdPolicyInfo](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicySelector.html) | Interfaccia che definisce le proprietà per le chiamate API `AdPolicySelector`. Queste proprietà forniscono il contesto per l&#39;imposizione di ogni comportamento annuncio. |
| [AdPolicySelector](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicySelector.html) | Un&#39;interfaccia di selezione criteri per l&#39;annuncio da applicare. Le applicazioni possono essere conformi a questa interfaccia implementando tutti i metodi richiesti o estendendo la classe di selezione dei criteri predefinita esistente per personalizzare comportamenti specifici. |
| [AdTimelineItem](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdTimelineItem.html) | Elemento della timeline associato a un annuncio specifico. |
| [AuditudeAdResolver](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AuditudeAdResolver.html) | Classe che gestisce la risoluzione di annunci in primetime nel processo TVSDK. |
| [AdType](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdType.html) | Enumerazione di tutti i tipi di annunci supportati da TVSDK. |
| [MetadataAdResolver](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/MetadataAdResolver.html) | Classe. |

