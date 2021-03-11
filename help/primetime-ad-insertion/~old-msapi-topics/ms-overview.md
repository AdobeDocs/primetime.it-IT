---
description: Il server manifest coordina i sistemi che forniscono contenuto, forniscono annunci, riproduci video e tieni traccia degli annunci. Riceve playlist codificate M3U8 (manifesti) che i lettori video client ricevono da fornitori di contenuti, unisce gli annunci dei fornitori di annunci nei manifesti e trasmette i manifesti uniti ai lettori video. Supporta sia il tracciamento degli annunci lato client che lato server. Esegue le sue interazioni utilizzando un'interfaccia di servizio Web basata su HTTP.
title: Panoramica delle interazioni server manifest
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 0%

---


# Panoramica delle interazioni server manifesto {#overview-of-manifest-server-interactions}

Il server manifest coordina i sistemi che forniscono contenuto, forniscono annunci, riproduci video e tieni traccia degli annunci. Riceve playlist codificate M3U8 (manifesti) che i lettori video client ricevono da fornitori di contenuti, unisce gli annunci dei fornitori di annunci nei manifesti e trasmette i manifesti uniti ai lettori video. Supporta sia il tracciamento degli annunci lato client che lato server. Esegue le sue interazioni utilizzando un&#39;interfaccia di servizio Web basata su HTTP.

Una configurazione tipica contiene:

* Server manifesto Primetime
* Primetime Creative Repackaging Service (CRS)
* Un client che controlla un lettore video
* Un editore, di solito con Content Management System (CMS)
* Una rete CDN (Content Delivery Network)
* Un server di annunci
* Ricevitore per report di tracciamento annunci

Il flusso di lavoro varia in base a una serie di fattori, ad esempio se la rete CDN è Akamai o se il client esegue il tracciamento degli annunci. Per un diagramma del flusso di lavoro per il tracciamento degli annunci lato client, consulta [Flusso di lavoro di tracciamento lato client](/help/primetime-ad-insertion/~old-msapi-topics/ms-at-effectiveness/notvsdk-csat-overview.md#section_cst_flow).

Il server manifest interagisce con i client di distribuzione video ricevendo e rispondendo alle richieste HTTP GET. Le risposte sono manifesti codificati M3U8 che descrivono contenuti ad-stitched, includendo facoltativamente una struttura JSON o VMAP (sidecar) contenente istruzioni dettagliate di tracciamento degli annunci (vedi [Formati di file](/help/primetime-ad-insertion/~old-msapi-topics/ms-list-file-formats/ms-api-file-formats.md)).

Un flusso di lavoro tipico si presenta come segue:

1. L’editore invia al client l’URL del contenuto e le informazioni per l’ad server.
1. Il client utilizza le informazioni dell&#39;editore per generare un URL del server manifesto e invia una richiesta di GET a tale URL. Questo è noto come URL Bootstrap.
1. Il server manifesto stabilisce una sessione con il client.
1. Il server manifest ottiene i manifesti di contenuto dalla CDN, che possono includere informazioni di interruzione di annunci.
1. Il server manifesto reindirizza il client al manifesto master/variante generato per il client.

   >[!NOTE]
   >
   >Se i parametri di query dell&#39;URL di Bootstrap contengono l&#39;impostazione `pttrackingmode=simple` o `ptplayer=ios-mobileweb`, il server manifest restituisce l&#39;URL del manifesto master/variante in un oggetto JSON e il client invia una richiesta di GET a tale URL del manifesto di variante.

1. Il client sceglie un flusso nel manifesto di variante generato per la riproduzione, l&#39;invio di informazioni pubblicitarie al server manifesto.
1. Il server manifesto trasmette le informazioni fornite dal client al server degli annunci e riceve gli annunci e gli URL di tracciamento degli annunci dal server degli annunci. Se un annuncio fornito non è in formato HLS, il server manifesto lo invia a CRS per la conversione a HLS.
1. Il server manifest unisce gli annunci nel manifesto del contenuto e invia il nuovo manifesto con unione al client.
1. Il client riproduce il contenuto con gli annunci uniti ed effettua le richieste nei momenti specificati agli URL di tracciamento specificati.

L&#39;inserimento di annunci di Primetime supporta i client su molte piattaforme di distribuzione video. Non tutti i client sono generati sul pacchetto TVSDK di Primetime, ma tutti i client inviano richieste GET allo stesso URL di base. I parametri di query distinguono una richiesta client da un&#39;altra indicando al server manifest:

* il cliente che effettua la richiesta,
* che cosa vuole quel cliente?
* e quali informazioni di tracciamento degli annunci fornire.

## CORS {#section_BEA7F298660944BE92801E4C82FCD038}

Il server manifesto utilizza lo standard CORS (Cross-Origin Resource Sharing). Cerca un&#39;intestazione `Origin` nelle richieste che riceve. Se l’intestazione è presente, risponde con

* `Access-Control-Allow-Origin: *`dall&#39;intestazione Origin`*`
* `Access-Control-Allow-Credentials: true`
* `Access-Control-Allow-Methods: GET`

In caso contrario, risponde con:

* `Access-Control-Allow-Origin: *`
* `Access-Control-Allow-Methods: GET`