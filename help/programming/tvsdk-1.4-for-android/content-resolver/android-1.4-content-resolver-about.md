---
description: Un rilevatore di opportunità è un componente TVSDK che rileva i tag personalizzati in un flusso e identifica le opportunità di posizionamento. Queste opportunità vengono inviate al resolver dei contenuti, che personalizza il flusso di lavoro di inserimento di contenuti/annunci in base alle proprietà e ai metadati dell’opportunità di posizionamento.
title: Generatori di opportunità e risolutori di contenuti
exl-id: e396eaa9-444d-4173-a534-74b29309a151
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 0%

---

# Generatori di opportunità e risolutori di contenuti {#opportunity-generators-and-content-resolvers}

Un rilevatore di opportunità è un componente TVSDK che rileva i tag personalizzati in un flusso e identifica le opportunità di posizionamento. Queste opportunità vengono inviate al resolver dei contenuti, che personalizza il flusso di lavoro di inserimento di contenuti/annunci in base alle proprietà e ai metadati dell’opportunità di posizionamento.

TVSDK include un rilevatore di opportunità predefinito:

* `SpliceOutPlacementOpportunityDetector`, che comprende i suggerimenti per annunci predefiniti

TVSDK include anche i resolver di contenuto predefiniti che forniscono il contenuto da inserire in base alla chiave di metadati nell’elemento del lettore:

* `AuditudeResolver` per `AUDITUDE_METADATA_KEY`, che è in grado di comunicare con i server di Adobe Primetime ad decisioning (precedentemente noti come Auditude) e di restituire le interruzioni pubblicitarie da inserire.

* `MetadataResolver` per `JSON_METADATA_KEY`

* `CustomAdMarkersContentResolver` per `TIME_RANGES_METADATA_KEY`

Puoi sovrascrivere i rilevatori di opportunità e i risolutori di contenuto predefiniti per personalizzare il flusso di lavoro della pubblicità nei seguenti modi:

* Aggiunta del supporto per il rilevamento di tag personalizzati
* Riconoscere tag personalizzati per l’inserimento di annunci
* Creare un provider di annunci personalizzato
* Contenuto in black out

TVSDK fornisce generatori di opportunità e resolver di contenuto predefiniti che inseriscono annunci nella timeline e questi generatori e resolver si basano su tag non standard nel manifesto. Potrebbe essere necessario modificare la timeline in base alle opportunità identificate nel manifesto, ad esempio gli indicatori per un periodo di sospensione attività.

Un *`opportunity`* rappresenta un punto di interesse sulla timeline che in genere indica un’opportunità di posizionamento di un annuncio. Questa opportunità può anche indicare un’operazione personalizzata che potrebbe influenzare la timeline, ad esempio un periodo di sospensione attività. Un *`opportunity generator`* identifica opportunità specifiche (tag) nella timeline e notifica a TVSDK che a tali opportunità sono stati assegnati dei tag. Le opportunità vengono identificate in una timeline in includendo un tag non standard (non HLS).

Quando l’applicazione riceve una notifica relativa a un’opportunità (tag), potrebbe modificare la timeline inserendo, ad esempio, una serie di annunci, passando a un flusso alternativo (sospensioni attività) o modificando in altro modo il contenuto della timeline. Per impostazione predefinita, TVSDK chiama il *`content resolver`* per implementare le modifiche o le azioni della sequenza temporale richieste. L&#39;applicazione può utilizzare il risolutore contenuto pubblicità TVSDK predefinito o registrare il proprio risolutore contenuto.

Puoi anche utilizzare `MediaPlayerItemConfig.setAdTags` per aggiungere altri tag/segnali di marcatura annuncio in modo che TVSDK possa riconoscerli e utilizzarli `MediaPlayerItemConfig.subscribedTags` e notifica all’applicazione eventuali tag aggiuntivi con informazioni sul flusso di lavoro della pubblicità.

Un possibile utilizzo di un risolutore personalizzato è per i periodi di sospensione attività. Per gestire questi periodi, l&#39;applicazione potrebbe implementare e registrare un rilevatore di opportunità di sospensione attività responsabile della gestione dei tag di sospensione attività. Quando TVSDK rileva questo tag, esegue il polling di tutti i risolutori di contenuto registrati per trovare il primo che gestisce il tag specificato. In questo esempio, è il risolutore del contenuto della sospensione attività che può, ad esempio, sostituire l’elemento corrente con contenuto alternativo sul lettore per la durata specificata dal tag.
