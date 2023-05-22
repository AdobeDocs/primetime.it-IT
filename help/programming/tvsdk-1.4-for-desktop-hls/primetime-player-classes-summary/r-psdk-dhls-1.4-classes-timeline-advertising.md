---
description: Queste classi forniscono informazioni sugli annunci che si verificano in una timeline.
title: Classi di pubblicità Timeline
exl-id: 2ac1f6b7-48b2-4d9c-b39d-a7e6f1ff2ac5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 0%

---

# Classi di pubblicità Timeline {#timeline-advertising-classes}

Queste classi forniscono informazioni sugli annunci che si verificano in una timeline.

Pacchetto [com.adobe.mediacore.timeline.advertising](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/package-detail.html)
Pacchetto [com.adobe.mediacore.timeline.advertising.policy](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/package-detail.html)

| Nome | Descrizione |
|---|---|
| [Annuncio](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/Ad.html) | Classe che definisce l’astrazione dell’annuncio e contiene tutte le informazioni sull’annuncio. È definito da un ID univoco, una durata e un `MediaResource`. Il `MediaResource` contiene l’URL in cui risiede il contenuto dell’annuncio effettivo. |
| [AdAsset](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdAsset.html) | Classe che rappresenta una risorsa da visualizzare. Classe che rappresenta una risorsa annuncio. |
| [AdBreak](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdBreak.html) | Classe che offre una visualizzazione unificata su diversi annunci che verranno riprodotti ad un certo punto durante la riproduzione. |
| [AdBreakPolicy](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdBreakPolicy.html) | Enumerazione che definisce il criterio di riproduzione dell’annuncio relativo all’utente ignorando gli annunci durante la ricerca. |
| [AdBreakTimelineItem](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdBreakTimelineItem.html) | Elemento della timeline associato all’interruzione pubblicitaria specifica. |
| [AdBreakWatchedPolicy](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdBreakWatchedPolicy.html) | Classe di enumerazione per i possibili criteri su quando contrassegnare un’interruzione pubblicitaria come controllata. |
| [AdClick](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdClick.html) | Classe che rappresenta un’istanza di clic associata a una risorsa. Questa istanza contiene informazioni sull’URL di click-through e il titolo che può essere utilizzato per fornire ulteriori informazioni all’utente. |
| [AdPolicy](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicy.html) | Classe di enumerazione per i criteri possibili su dove riprendere la riproduzione di un’interruzione pubblicitaria dopo la ricerca o la modalità di riproduzione con trucco. |
| [AdPolicyMode](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicyMode.html) | Classe di enumerazione che elenca i modi in cui il lettore viene riprodotto, ad esempio ricerca o riproduzione normale. |
| [AdPolicyInfo](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicySelector.html) | Interfaccia che definisce le proprietà per `AdPolicySelector` Chiamate API. Queste proprietà forniscono il contesto per applicare ogni comportamento pubblicitario. |
| [AdPolicySelector](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicySelector.html) | Un’interfaccia del selettore dei criteri degli annunci per applicare i comportamenti degli annunci. Le applicazioni possono conformarsi a questa interfaccia implementando tutti i metodi richiesti o estendendo la classe del selettore dei criteri predefinita esistente per personalizzare comportamenti specifici. |
| [AdTimelineItem](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdTimelineItem.html) | Elemento della timeline associato a un annuncio specifico. |
| [AuditudeAdResolver](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AuditudeAdResolver.html) | Classe che gestisce la risoluzione degli annunci di prima serata nel processo TVSDK. |
| [AdType](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdType.html) | Enumerazione di tutti i tipi di annunci supportati da TVSDK. |
| [MetadataAdResolution](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/MetadataAdResolver.html) | Classe. |
