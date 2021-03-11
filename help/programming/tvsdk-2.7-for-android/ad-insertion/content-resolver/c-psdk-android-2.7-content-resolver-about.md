---
description: TVSDK fornisce generatori di opportunità e risolutori di contenuti predefiniti che inseriscono gli annunci nella timeline e questi generatori e risolutori si basano su tag non standard nel manifesto. L'applicazione potrebbe dover modificare la cronologia in base alle opportunità identificate nel manifesto, ad esempio gli indicatori per un periodo di sospensione attività.
title: Generatori di opportunità e risolutori di contenuti
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 0%

---


# Generatori di opportunità e risolutori di contenuti {#opportunity-generators-and-content-resolvers}

TVSDK fornisce generatori di opportunità e risolutori di contenuti predefiniti che inseriscono gli annunci nella timeline e questi generatori e risolutori si basano su tag non standard nel manifesto. L&#39;applicazione potrebbe dover modificare la cronologia in base alle opportunità identificate nel manifesto, ad esempio gli indicatori per un periodo di sospensione attività.

Un *`opportunity`* rappresenta un punto di interesse sulla timeline che in genere indica un’opportunità di posizionamento di annunci. Questa opportunità può anche indicare un’operazione personalizzata che potrebbe influenzare la timeline, ad esempio un periodo di sospensione attività. Un *`opportunity generator`* identifica opportunità specifiche (tag) nella timeline e notifica a TVSDK che queste opportunità sono state contrassegnate. Le opportunità sono identificate in una timeline in includendo un tag non standard (non HLS).

Quando l&#39;applicazione viene informata di un&#39;opportunità, l&#39;applicazione potrebbe modificare la timeline inserendo una serie di annunci, passando a un flusso alternativo (blackout) o modificando in altro modo il contenuto della timeline. Per impostazione predefinita, il TVSDK chiama il *`content resolver`* appropriato per implementare le modifiche o le azioni della timeline richieste. L’applicazione può utilizzare il risolutore di contenuto dell’annuncio TVSDK predefinito o registrare il proprio risolutore di contenuto.

Puoi inoltre utilizzare `MediaPlayerItemConfig.setAdTags` per aggiungere altri tag/suggerimenti per gli indicatori di annunci in modo che TVSDK possa riconoscere e utilizzare `MediaPlayerItemConfig.subscribedTags` e inviare una notifica all’applicazione per eventuali tag aggiuntivi con informazioni sul flusso di lavoro pubblicitario.

Un possibile utilizzo di un risolutore personalizzato è per i periodi di blackout. Per gestire questi periodi, l’applicazione può implementare e registrare un rilevatore di opportunità di blackout responsabile della gestione dei tag di blackout. Quando TVSDK rileva questo tag, esegue il polling di tutti i resolver di contenuti registrati per trovare il primo che gestisce il tag specificato. In questo esempio, è il risolutore di contenuti in sospensione, che può, ad esempio, sostituire l&#39;elemento corrente con contenuto alternativo sul lettore per la durata specificata dal tag.
