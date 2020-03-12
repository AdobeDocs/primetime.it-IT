---
description: Un rilevatore di opportunità è un componente TVSDK che rileva i tag personalizzati in un flusso e identifica le opportunità di posizionamento. Queste opportunità vengono inviate al risolutore dei contenuti, che personalizzerà il flusso di lavoro di inserimento dei contenuti/annunci in base alle proprietà delle opportunità di posizionamento e ai metadati.
seo-description: Un rilevatore di opportunità è un componente TVSDK che rileva i tag personalizzati in un flusso e identifica le opportunità di posizionamento. Queste opportunità vengono inviate al risolutore dei contenuti, che personalizzerà il flusso di lavoro di inserimento dei contenuti/annunci in base alle proprietà delle opportunità di posizionamento e ai metadati.
seo-title: Generatori di opportunità e risolutori di contenuti
title: Generatori di opportunità e risolutori di contenuti
uuid: c49494da-2145-40d7-8f4b-2ecaf2866ca4
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# Generatori di opportunità e risolutori di contenuti {#opportunity-generators-and-content-resolvers}

Un rilevatore di opportunità è un componente TVSDK che rileva i tag personalizzati in un flusso e identifica le opportunità di posizionamento. Queste opportunità vengono inviate al risolutore dei contenuti, che personalizzerà il flusso di lavoro di inserimento dei contenuti/annunci in base alle proprietà delle opportunità di posizionamento e ai metadati.

TVSDK include un rilevatore di opportunità predefinito:

* `PTOpportunityResolver`, che comprende i segnali di annunci predefiniti

TVSDK include anche un risolutore di contenuto predefinito che fornisce il contenuto da inserire in base alla chiave di metadati nell&#39;elemento del lettore:

* `PTContentResolver`

Potete ignorare i rilevatori di opportunità e i risolutori di contenuti predefiniti per personalizzare il flusso di lavoro pubblicitario nei seguenti modi:

* Supporto aggiuntivo per il rilevamento tag personalizzato
* Riconoscere i tag personalizzati per l&#39;inserimento di annunci
* Creare un provider di annunci personalizzato
* Contenuto BlackOut

<!--<a id="section_C2BA8F50230E4010ABFCD5D976BC1217"></a>-->

TVSDK fornisce generatori di opportunità e risolutori di contenuti predefiniti che inseriscono annunci nella timeline, e questi generatori e risolutori sono basati su tag non standard nel manifesto. L&#39;applicazione potrebbe dover modificare la cronologia in base alle opportunità identificate nel manifesto, ad esempio gli indicatori per un periodo di blackout.

Un *`opportunity`* rappresenta un punto di interesse sulla timeline che in genere indica un&#39;opportunità di posizionamento degli annunci. Questa opportunità può anche indicare un&#39;operazione personalizzata che potrebbe influenzare la cronologia, ad esempio un periodo di sospensione attività. An *`opportunity generator`* identifica opportunità specifiche (tag) nella timeline e notifica a TVSDK che queste opportunità sono state contrassegnate con tag. Le opportunità sono identificate in una timeline `PTTimedMetadata` includendo un tag non standard (non HLS).

Quando all&#39;applicazione viene notificato un&#39;opportunità (tag), l&#39;applicazione potrebbe modificare la timeline, ad esempio inserendo una serie di annunci, passando a un flusso alternativo (blackout) o modificando in altro modo il contenuto della timeline. Per impostazione predefinita, TVSDK chiama il metodo appropriato *`content resolver`* per implementare le modifiche o le azioni della cronologia richieste. L’applicazione può utilizzare il risolutore di contenuto dell’annuncio TVSDK predefinito o registrare un proprio risolutore di contenuto.

Potete anche utilizzare `PTSDKConfig.setAdTags` per aggiungere altri tag/suggerimenti per gli indicatori di annunci in modo che TVSDK possa riconoscere e utilizzare `PTSDKConfig.setSubscribedTags` e notificare all’applicazione altri tag che potrebbero includere informazioni sul flusso di lavoro pubblicitario.

Un possibile utilizzo di un risolutore personalizzato è per i periodi di blackout. Per gestire questi periodi, l&#39;applicazione potrebbe implementare e registrare un rilevatore di opportunità blackout responsabile per la gestione dei tag blackout. Quando TVSDK rileva questo tag, esegue il polling di tutti i risolutori di contenuto registrati per trovare il primo che gestisce il tag specificato. In questo esempio, è il risolutore di contenuto blackout, che può, ad esempio, sostituire l&#39;elemento corrente con contenuto alternativo sul lettore per la durata specificata dal tag.