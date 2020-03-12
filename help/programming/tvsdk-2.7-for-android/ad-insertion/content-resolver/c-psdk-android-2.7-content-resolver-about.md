---
description: TVSDK fornisce generatori di opportunità e risolutori di contenuti predefiniti che inseriscono annunci nella timeline, e questi generatori e risolutori sono basati su tag non standard nel manifesto. L'applicazione potrebbe dover modificare la cronologia in base alle opportunità identificate nel manifesto, ad esempio gli indicatori per un periodo di blackout.
seo-description: TVSDK fornisce generatori di opportunità e risolutori di contenuti predefiniti che inseriscono annunci nella timeline, e questi generatori e risolutori sono basati su tag non standard nel manifesto. L'applicazione potrebbe dover modificare la cronologia in base alle opportunità identificate nel manifesto, ad esempio gli indicatori per un periodo di blackout.
seo-title: Generatori di opportunità e risolutori di contenuti
title: Generatori di opportunità e risolutori di contenuti
uuid: 35823336-5338-4cdc-8778-e73cd1d05251
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# Generatori di opportunità e risolutori di contenuti {#opportunity-generators-and-content-resolvers}

TVSDK fornisce generatori di opportunità e risolutori di contenuti predefiniti che inseriscono annunci nella timeline, e questi generatori e risolutori sono basati su tag non standard nel manifesto. L&#39;applicazione potrebbe dover modificare la cronologia in base alle opportunità identificate nel manifesto, ad esempio gli indicatori per un periodo di blackout.

Un *`opportunity`* rappresenta un punto di interesse sulla timeline che in genere indica un&#39;opportunità di posizionamento degli annunci. Questa opportunità può anche indicare un&#39;operazione personalizzata che potrebbe influenzare la cronologia, ad esempio un periodo di sospensione attività. An *`opportunity generator`* identifica opportunità specifiche (tag) nella timeline e notifica a TVSDK che queste opportunità sono state contrassegnate con tag. Le opportunità sono identificate in una timeline in includendo un tag non standard (non HLS).

Quando l&#39;applicazione riceve una notifica su un&#39;opportunità, l&#39;applicazione potrebbe modificare la timeline inserendo una serie di annunci, passando a un flusso alternativo (blackout) o modificando in altro modo il contenuto della timeline. Per impostazione predefinita, TVSDK chiama il metodo appropriato *`content resolver`* per implementare le modifiche o le azioni della cronologia richieste. L’applicazione può utilizzare il risolutore di contenuto dell’annuncio TVSDK predefinito o registrare un proprio risolutore di contenuto.

Potete anche utilizzare `MediaPlayerItemConfig.setAdTags` per aggiungere altri tag/suggerimenti marcatore annunci in modo che TVSDK possa riconoscere e utilizzare `MediaPlayerItemConfig.subscribedTags` e notificare all’applicazione eventuali tag aggiuntivi con informazioni sul flusso di lavoro pubblicitario.

Un possibile utilizzo di un risolutore personalizzato è per i periodi di blackout. Per gestire questi periodi, l&#39;applicazione potrebbe implementare e registrare un rilevatore di opportunità blackout responsabile per la gestione dei tag blackout. Quando TVSDK rileva questo tag, esegue il polling di tutti i risolutori di contenuto registrati per trovare il primo che gestisce il tag specificato. In questo esempio, è il risolutore di contenuto blackout, che può, ad esempio, sostituire l&#39;elemento corrente con contenuto alternativo sul lettore per la durata specificata dal tag.
