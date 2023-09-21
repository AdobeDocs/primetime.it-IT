---
description: TVSDK fornisce generatori di opportunità e resolver di contenuto predefiniti che inseriscono annunci nella timeline e questi generatori e resolver si basano su tag non standard nel manifesto. Potrebbe essere necessario modificare la timeline in base alle opportunità identificate nel manifesto, ad esempio gli indicatori per un periodo di sospensione attività.
title: Generatori di opportunità e risolutori di contenuti
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 0%

---

# Generatori di opportunità e risolutori di contenuti {#opportunity-generators-and-content-resolvers}

TVSDK fornisce generatori di opportunità e resolver di contenuto predefiniti che inseriscono annunci nella timeline e questi generatori e resolver si basano su tag non standard nel manifesto. Potrebbe essere necessario modificare la timeline in base alle opportunità identificate nel manifesto, ad esempio gli indicatori per un periodo di sospensione attività.

Un *`opportunity`* rappresenta un punto di interesse sulla timeline che in genere indica un’opportunità di posizionamento di un annuncio. Questa opportunità può anche indicare un’operazione personalizzata che potrebbe influenzare la timeline, ad esempio un periodo di sospensione attività. Un *`opportunity generator`* identifica opportunità specifiche (tag) nella timeline e notifica a TVSDK che a tali opportunità sono stati assegnati dei tag. Le opportunità vengono identificate in una timeline in includendo un tag non standard (non HLS).

Quando all’applicazione viene inviata una notifica su un’opportunità, l’applicazione potrebbe modificare la timeline inserendo una serie di annunci, passando a un flusso alternativo (sospensioni attività) o modificando in altro modo il contenuto della timeline. Per impostazione predefinita, TVSDK chiama il *`content resolver`* per implementare le modifiche o le azioni della sequenza temporale richieste. L&#39;applicazione può utilizzare il risolutore contenuto pubblicità TVSDK predefinito o registrare il proprio risolutore contenuto.

Puoi anche utilizzare `MediaPlayerItemConfig.setAdTags` per aggiungere altri tag/segnali di marcatura annuncio in modo che TVSDK possa riconoscerli e utilizzarli `MediaPlayerItemConfig.subscribedTags` e notifica all’applicazione eventuali tag aggiuntivi con informazioni sul flusso di lavoro della pubblicità.

Un possibile utilizzo di un risolutore personalizzato è per i periodi di sospensione attività. Per gestire questi periodi, l&#39;applicazione potrebbe implementare e registrare un rilevatore di opportunità di sospensione attività responsabile della gestione dei tag di sospensione attività. Quando TVSDK rileva questo tag, esegue il polling di tutti i risolutori di contenuto registrati per trovare il primo che gestisce il tag specificato. In questo esempio, è il risolutore del contenuto della sospensione attività che può, ad esempio, sostituire l’elemento corrente con contenuto alternativo sul lettore per la durata specificata dal tag.
