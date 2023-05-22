---
description: Il server manifest coordina i sistemi che forniscono contenuti, annunci pubblicitari, riproduzione video e tracciamento degli annunci. Riceve playlist (manifesti) con codifica M3U8 che i lettori video client ricevono dai provider di contenuti, unisce gli annunci dei provider di annunci nei manifesti e trasmette i manifesti uniti ai lettori video. Supporta sia il tracciamento degli annunci lato client che lato server. Esegue le interazioni utilizzando un’interfaccia di servizio web basata su HTTP.
title: Panoramica delle interazioni di Manifest Server
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 0%

---


# Panoramica delle interazioni di Manifest Server {#overview-of-manifest-server-interactions}

Il server manifest coordina i sistemi che forniscono contenuti, annunci pubblicitari, riproduzione video e tracciamento degli annunci. Riceve playlist (manifesti) con codifica M3U8 che i lettori video client ricevono dai provider di contenuti, unisce gli annunci dei provider di annunci nei manifesti e trasmette i manifesti uniti ai lettori video. Supporta sia il tracciamento degli annunci lato client che lato server. Esegue le interazioni utilizzando un’interfaccia di servizio web basata su HTTP.

Una configurazione tipica contiene:

* Il server manifest di Primetime
* Servizio di riconfezionamento creativo di Primetime (CRS)
* Un client che controlla un lettore video
* Un editore, in genere con un sistema di gestione dei contenuti (CMS)
* Una rete per la distribuzione dei contenuti (CDN)
* Un ad server
* Un ricevitore per i rapporti di tracciamento degli annunci

Il flusso di lavoro varia in base a una serie di fattori, ad esempio se la rete CDN è Akamai o se il client esegue il tracciamento degli annunci. Per un diagramma del flusso di lavoro per il tracciamento degli annunci lato client, vedi [Flusso di lavoro di tracciamento lato client](/help/primetime-ad-insertion/~old-msapi-topics/ms-at-effectiveness/notvsdk-csat-overview.md#section_cst_flow).

Il server manifest interagisce con i client di consegna video ricevendo e rispondendo alle richieste HTTP GET. Le risposte sono manifesti con codifica M3U8 che descrivono contenuti ad-stitched, facoltativamente includendo una struttura JSON o VMAP (sidecar) contenente istruzioni dettagliate per il tracciamento degli annunci (vedi [Formati di file](/help/primetime-ad-insertion/~old-msapi-topics/ms-list-file-formats/ms-api-file-formats.md)).

Un flusso di lavoro tipico si presenta come segue:

1. L’editore invia l’URL del contenuto e le informazioni per l’ad server al client.
1. Il client utilizza le informazioni dell&#39;editore per generare un URL del server manifesto e invia una richiesta di GET a tale URL. Questo è noto come URL di Bootstrap.
1. Il server manifesto stabilisce una sessione con il client.
1. Il server dei manifesti ottiene i manifesti di contenuto dalla rete CDN, che può includere informazioni sull’interruzione dell’annuncio.
1. Il server manifesto reindirizza il client al manifesto master/variante generato per il client.

   >[!NOTE]
   >
   >Se i parametri di query dell’URL di Bootstrap contengono `pttrackingmode=simple` o `ptplayer=ios-mobileweb` , il server manifesto restituisce l’URL del manifesto master/variante in un oggetto JSON e il client invia una richiesta GET a tale URL del manifesto variante.

1. Il client sceglie un flusso nel manifesto della variante generato da riprodurre, inviando informazioni sull’annuncio al server del manifesto.
1. Il server manifesto trasmette le informazioni fornite dal client al server di annunci e riceve gli annunci e gli URL di tracciamento degli annunci dal server di annunci. Se un annuncio fornito non è in formato HLS, il server manifest lo invia a CRS per la conversione in HLS.
1. Il server manifesto unisce gli annunci nel manifesto del contenuto e invia il nuovo manifesto unito al client.
1. Il client riproduce il contenuto con gli annunci uniti e invia richieste agli URL di tracciamento specificati, nei momenti specificati.

L’inserimento di annunci Primetime supporta i client su molte piattaforme di distribuzione di video. Non tutti i client sono basati sul pacchetto TVSDK di Primetime, ma tutti inviano richieste GET allo stesso URL di base. I parametri di query distinguono una richiesta client da un’altra indicando al server manifesto:

* il cliente che effettua la richiesta,
* quello che vuole quel cliente,
* e quali informazioni di tracciamento degli annunci fornire.

## CORS {#section_BEA7F298660944BE92801E4C82FCD038}

Il server manifest utilizza lo standard CORS (Cross-Origin Resource Sharing). Cerca un `Origin` nelle richieste che riceve. Se l’intestazione è presente, risponde con

* `Access-Control-Allow-Origin: *`stringa dall’intestazione Origin`*`
* `Access-Control-Allow-Credentials: true`
* `Access-Control-Allow-Methods: GET`

In caso contrario, risponde con:

* `Access-Control-Allow-Origin: *`
* `Access-Control-Allow-Methods: GET`