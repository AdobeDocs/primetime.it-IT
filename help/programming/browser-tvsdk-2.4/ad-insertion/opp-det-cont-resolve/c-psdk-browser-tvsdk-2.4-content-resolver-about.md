---
description: Browser TVSDK fornisce generatori di opportunità e resolver di contenuto predefiniti che inseriscono annunci nella timeline. Questi generatori e resolver si basano su tag non standard nel manifesto. L’applicazione potrebbe dover modificare la timeline in base alle opportunità identificate nel manifesto.
title: Generatori di opportunità e risolutori di contenuti
exl-id: a47acd22-8b1b-4c66-a7eb-a4d99afb5f17
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---

# Generatori di opportunità e risolutori di contenuti{#opportunity-generators-and-content-resolvers}

Browser TVSDK fornisce generatori di opportunità e resolver di contenuto predefiniti che inseriscono annunci nella timeline. Questi generatori e resolver si basano su tag non standard nel manifesto. L’applicazione potrebbe dover modificare la timeline in base alle opportunità identificate nel manifesto.

Un *`opportunity`* rappresenta un punto di interesse sulla timeline che in genere indica un’opportunità di posizionamento di un annuncio. Questa opportunità può anche indicare un’operazione personalizzata che potrebbe influenzare la timeline. Un *`opportunity generator`* identifica opportunità specifiche (tag) nella timeline e notifica a TVSDK che a tali opportunità sono stati assegnati dei tag.

Le opportunità vengono identificate in una timeline in `TimedMetata`. Il `ManifestCuesOpportunityGenerator` crea opportunità basate su `TimedMetadata` oggetti creati per ogni tag annuncio di giunzione (in `MediaPlayerItemConfig.adTags`) rilevato nel manifesto. Il `AdSignalingModeOpportunityGenerator` crea l&#39;opportunità iniziale basata su `MediaPlayerItem` il tipo e la modalità di segnalazione pubblicitaria associata.

>[!TIP]
>
>Se il `AdvertisingMetadata.livePreroll` o `AdvertisingMetadata.preroll` proprietà impostata, `AdSignalingModeOpportunityGenerator` genera un’opportunità di pre-roll per i flussi live.

Quando l’applicazione riceve una notifica relativa a un’opportunità (tag), l’applicazione potrebbe modificare la timeline, ad esempio, inserendo una serie di annunci. Per impostazione predefinita, il TVSDK del browser chiama il *`content resolver`* per implementare le modifiche o le azioni della sequenza temporale richieste. La tua applicazione può utilizzare il browser predefinito TVSDK advertising content resolver o registrare il proprio content resolver.

Puoi anche utilizzare `MediaPlayerItemConfig.adTags` per aggiungere altri tag/segnali di marcatura annuncio per il valore predefinito `ManifestCuesOpportunityGenerator` classe e utilizzo `MediaPlayerItemConfig.subscribedTags` in modo che TVSDK possa notificare all’applicazione eventuali tag aggiuntivi con informazioni sul flusso di lavoro pubblicitario.

>[!TIP]
>
>I valori predefiniti di `MediaPlayerItemConfig.adTags` e `MediaPlayerItemConfig.subscribeTags` è `[MediaPlayerItemConfig.DEFAULT_AD_TAG]`.
