---
description: Browser TVSDK fornisce generatori di opportunità e risolutori di contenuti predefiniti che inseriscono annunci nella timeline, e questi generatori e risolutori sono basati su tag non standard nel manifesto. L'applicazione potrebbe dover modificare la cronologia in base alle opportunità identificate nel manifesto.
seo-description: Browser TVSDK fornisce generatori di opportunità e risolutori di contenuti predefiniti che inseriscono annunci nella timeline, e questi generatori e risolutori sono basati su tag non standard nel manifesto. L'applicazione potrebbe dover modificare la cronologia in base alle opportunità identificate nel manifesto.
seo-title: Generatori di opportunità e risolutori di contenuti
title: Generatori di opportunità e risolutori di contenuti
uuid: e462ad89-1609-4efa-aa67-cfd04f045927
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---


# Generatori di opportunità e risolutori di contenuti{#opportunity-generators-and-content-resolvers}

Browser TVSDK fornisce generatori di opportunità e risolutori di contenuti predefiniti che inseriscono annunci nella timeline, e questi generatori e risolutori sono basati su tag non standard nel manifesto. L&#39;applicazione potrebbe dover modificare la cronologia in base alle opportunità identificate nel manifesto.

Un *`opportunity`* rappresenta un punto di interesse sulla timeline che in genere indica un&#39;opportunità di posizionamento per gli annunci. Questa opportunità può anche indicare un&#39;operazione personalizzata che potrebbe influenzare la cronologia. Un *`opportunity generator`* identifica opportunità specifiche (tag) nella timeline e notifica a TVSDK che queste opportunità sono state contrassegnate con tag.

Le opportunità sono identificate in una timeline in `TimedMetata`. Il `ManifestCuesOpportunityGenerator` crea opportunità in base agli oggetti `TimedMetadata` creati per ciascun tag ad out (in `MediaPlayerItemConfig.adTags`) rilevato nel manifesto. L&#39; `AdSignalingModeOpportunityGenerator` crea l&#39;opportunità iniziale basata sul tipo `MediaPlayerItem` e sulla relativa modalità di segnalazione annunci associata.

>[!TIP]
>
>Se la proprietà `AdvertisingMetadata.livePreroll` o `AdvertisingMetadata.preroll` è impostata, `AdSignalingModeOpportunityGenerator` genera un&#39;opportunità pre-roll per i flussi live.

Quando all&#39;applicazione viene notificato un&#39;opportunità (tag), l&#39;applicazione potrebbe modificare la cronologia inserendo, ad esempio, una serie di annunci. Per impostazione predefinita, Browser TVSDK chiama il *`content resolver`* appropriato per implementare le modifiche o le azioni della cronologia richieste. L&#39;applicazione può utilizzare il risolutore di contenuto dell&#39;annuncio TVSDK del browser predefinito o registrare un proprio risolutore di contenuto.

Potete anche utilizzare `MediaPlayerItemConfig.adTags` per aggiungere altri tag/suggerimenti per l&#39;indicatore di annunci per la classe `ManifestCuesOpportunityGenerator` predefinita e utilizzare `MediaPlayerItemConfig.subscribedTags` in modo che TVSDK possa inviare alla vostra applicazione notifiche su altri tag che potrebbero contenere informazioni sul flusso di lavoro pubblicitario.

>[!TIP]
>
>I valori predefiniti di `MediaPlayerItemConfig.adTags` e `MediaPlayerItemConfig.subscribeTags` sono `[MediaPlayerItemConfig.DEFAULT_AD_TAG]`.

