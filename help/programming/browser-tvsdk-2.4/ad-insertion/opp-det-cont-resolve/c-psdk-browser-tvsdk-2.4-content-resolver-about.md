---
description: Il browser TVSDK fornisce generatori di opportunità e risolutori di contenuti predefiniti che inseriscono gli annunci nella timeline e questi generatori e risolutori si basano su tag non standard nel manifesto. L'applicazione potrebbe dover modificare la cronologia in base alle opportunità identificate nel manifesto.
title: Generatori di opportunità e risolutori di contenuti
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---


# Generatori di opportunità e risolutori di contenuti{#opportunity-generators-and-content-resolvers}

Il browser TVSDK fornisce generatori di opportunità e risolutori di contenuti predefiniti che inseriscono gli annunci nella timeline e questi generatori e risolutori si basano su tag non standard nel manifesto. L&#39;applicazione potrebbe dover modificare la cronologia in base alle opportunità identificate nel manifesto.

Un *`opportunity`* rappresenta un punto di interesse sulla timeline che in genere indica un’opportunità di posizionamento di annunci. Questa opportunità può anche indicare un’operazione personalizzata che potrebbe influenzare la timeline. Un *`opportunity generator`* identifica opportunità specifiche (tag) nella timeline e notifica a TVSDK che queste opportunità sono state contrassegnate.

Le opportunità sono identificate in una timeline in `TimedMetata`. Il `ManifestCuesOpportunityGenerator` crea opportunità in base agli `TimedMetadata` oggetti creati per ogni tag di annuncio a comparsa (in `MediaPlayerItemConfig.adTags`) rilevato nel manifesto. L’ `AdSignalingModeOpportunityGenerator` crea l’opportunità iniziale basata sul tipo `MediaPlayerItem` e sulla relativa modalità di segnalazione degli annunci associata.

>[!TIP]
>
>Se è impostata la proprietà `AdvertisingMetadata.livePreroll` o `AdvertisingMetadata.preroll` , `AdSignalingModeOpportunityGenerator` genera un’opportunità pre-roll per i flussi live.

Quando l&#39;applicazione viene informata di un&#39;opportunità (tag), l&#39;applicazione potrebbe modificare la timeline inserendo, ad esempio, una serie di annunci. Per impostazione predefinita, il browser TVSDK chiama il *`content resolver`* appropriato per implementare le modifiche o le azioni della timeline richieste. L&#39;applicazione può utilizzare il risolutore di contenuti pubblicitari TVSDK del browser predefinito o registrare il proprio risolutore di contenuti.

Puoi inoltre utilizzare `MediaPlayerItemConfig.adTags` per aggiungere altri tag/suggerimenti per gli indicatori di annunci per la classe predefinita `ManifestCuesOpportunityGenerator` e utilizzare `MediaPlayerItemConfig.subscribedTags` in modo che TVSDK possa inviare alla tua applicazione notifiche su tag aggiuntivi che potrebbero avere informazioni sul flusso di lavoro pubblicitario.

>[!TIP]
>
>I valori predefiniti di `MediaPlayerItemConfig.adTags` e `MediaPlayerItemConfig.subscribeTags` sono `[MediaPlayerItemConfig.DEFAULT_AD_TAG]`.

