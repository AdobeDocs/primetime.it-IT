---
description: Browser TVSDK fornisce generatori di opportunità e risolutori di contenuti predefiniti che inseriscono annunci nella timeline, e questi generatori e risolutori sono basati su tag non standard nel manifesto. L'applicazione potrebbe dover modificare la cronologia in base alle opportunità identificate nel manifesto.
seo-description: Browser TVSDK fornisce generatori di opportunità e risolutori di contenuti predefiniti che inseriscono annunci nella timeline, e questi generatori e risolutori sono basati su tag non standard nel manifesto. L'applicazione potrebbe dover modificare la cronologia in base alle opportunità identificate nel manifesto.
seo-title: Generatori di opportunità e risolutori di contenuti
title: Generatori di opportunità e risolutori di contenuti
uuid: e462ad89-1609-4efa-aa67-cfd04f045927
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Generatori di opportunità e risolutori di contenuti{#opportunity-generators-and-content-resolvers}

Browser TVSDK fornisce generatori di opportunità e risolutori di contenuti predefiniti che inseriscono annunci nella timeline, e questi generatori e risolutori sono basati su tag non standard nel manifesto. L&#39;applicazione potrebbe dover modificare la cronologia in base alle opportunità identificate nel manifesto.

Un *`opportunity`* rappresenta un punto di interesse sulla timeline che in genere indica un&#39;opportunità di posizionamento degli annunci. Questa opportunità può anche indicare un&#39;operazione personalizzata che potrebbe influenzare la cronologia. An *`opportunity generator`* identifica opportunità specifiche (tag) nella timeline e notifica a TVSDK che queste opportunità sono state contrassegnate con tag.

Le opportunità sono identificate in una timeline in `TimedMetata`. Questo `ManifestCuesOpportunityGenerator` crea opportunità in base agli `TimedMetadata` oggetti creati per ciascun tag ad uscita (in `MediaPlayerItemConfig.adTags`) rilevato nel manifesto. Crea `AdSignalingModeOpportunityGenerator` l’opportunità iniziale basata sul `MediaPlayerItem` tipo e sulla modalità di segnalazione ad essa associata.

>[!TIP]
>
>Se la `AdvertisingMetadata.livePreroll` proprietà o la `AdvertisingMetadata.preroll` proprietà è impostata, `AdSignalingModeOpportunityGenerator` genera un&#39;opportunità pre-roll per i flussi live.

Quando all&#39;applicazione viene notificato un&#39;opportunità (tag), l&#39;applicazione potrebbe modificare la cronologia inserendo, ad esempio, una serie di annunci. Per impostazione predefinita, Browser TVSDK chiama il metodo appropriato *`content resolver`* per implementare le modifiche o le azioni della cronologia richieste. L&#39;applicazione può utilizzare il risolutore di contenuto dell&#39;annuncio TVSDK del browser predefinito o registrare un proprio risolutore di contenuto.

Potete anche utilizzare `MediaPlayerItemConfig.adTags` per aggiungere altri tag/suggerimenti per l&#39;indicatore di annunci per la `ManifestCuesOpportunityGenerator` classe predefinita e per utilizzare `MediaPlayerItemConfig.subscribedTags` in modo che TVSDK possa notificare all&#39;applicazione altri tag che potrebbero contenere informazioni sul flusso di lavoro della pubblicità.

>[!TIP]
>
>I valori predefiniti di `MediaPlayerItemConfig.adTags` e `MediaPlayerItemConfig.subscribeTags` è `[MediaPlayerItemConfig.DEFAULT_AD_TAG]`.

