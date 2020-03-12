---
description: Il server del manifesto coordina i sistemi che forniscono contenuto, forniscono annunci pubblicitari, riproducono video e tracciano annunci. Riceve playlist codificate M3U8 (manifesti) che i lettori video client ricevono da fornitori di contenuti, cuoce annunci da fornitori di annunci nei manifesti e trasmette i manifesti cuciti ai lettori video. Supporta sia il monitoraggio degli annunci lato client che lato server. Esegue le proprie interazioni tramite un'interfaccia di servizio Web basata su HTTP.
seo-description: Il server del manifesto coordina i sistemi che forniscono contenuto, forniscono annunci pubblicitari, riproducono video e tracciano annunci. Riceve playlist codificate M3U8 (manifesti) che i lettori video client ricevono da fornitori di contenuti, cuoce annunci da fornitori di annunci nei manifesti e trasmette i manifesti cuciti ai lettori video. Supporta sia il monitoraggio degli annunci lato client che lato server. Esegue le proprie interazioni tramite un'interfaccia di servizio Web basata su HTTP.
seo-title: Panoramica delle interazioni del server manifesto
title: Panoramica delle interazioni del server manifesto
uuid: 3e314a45-a4dd-492f-8915-19224a8fbbc7
translation-type: tm+mt
source-git-commit: 9dc8498593a1d70918b66016e429eb013cdc61f7

---


# Panoramica delle interazioni del server manifesto {#overview-of-manifest-server-interactions}

Il server del manifesto coordina i sistemi che forniscono contenuto, forniscono annunci pubblicitari, riproducono video e tracciano annunci. Riceve playlist codificate M3U8 (manifesti) che i lettori video client ricevono da fornitori di contenuti, cuoce annunci da fornitori di annunci nei manifesti e trasmette i manifesti cuciti ai lettori video. Supporta sia il monitoraggio degli annunci lato client che lato server. Esegue le proprie interazioni tramite un&#39;interfaccia di servizio Web basata su HTTP.

Una configurazione tipica contiene:

* Server manifesto Primetime
* Primetime Creative Repackaging Service (CRS)
* Un client, controllo di un lettore video
* Un editore, in genere con Content Management System (CMS)
* Una rete CDN (Content Delivery Network)
* Un server di annunci
* Ricevitore per report di tracciamento annunci

Il flusso di lavoro varia in base a una serie di fattori, ad esempio se la rete CDN è Akamai o se il client esegue il tracciamento degli annunci. Per un diagramma del flusso di lavoro per il tracciamento degli annunci lato client, consultate Flusso di lavoro [di tracciamento lato](../msapi-topics/ms-at-effectiveness/notvsdk-csat-overview.md#section_cst_flow)client.

Il server manifesto interagisce con i client di distribuzione video ricevendo e rispondendo alle richieste HTTP GET. Le risposte sono manifesti codificati con M3U8 che descrivono contenuti ad-stitched, facoltativamente inclusi una struttura JSON o VMAP (sidecar) contenente istruzioni dettagliate per il tracciamento degli annunci (consultate Formati [di](../msapi-topics/ms-list-file-formats/ms-api-file-formats.md)file).

Esempio di un flusso di lavoro tipico:

1. L&#39;editore invia al client l&#39;URL del contenuto e le informazioni per il server di annunci.
1. Il client utilizza le informazioni dell&#39;editore per generare un URL del server manifesto e invia una richiesta GET a tale URL. Questo è noto come URL di avvio.
1. Il server manifesto stabilisce una sessione con il client.
1. Il server del manifesto ottiene i manifesti di contenuto dalla rete CDN, che può includere informazioni sull’interruzione dell’annuncio.
1. Il server manifesto reindirizzerà il client al manifesto master/variante generato per il client.

   >[!NOTE]
   >
   >Se i parametri di query dell&#39;URL di avvio contengono l&#39;impostazione `pttrackingmode=simple` o `ptplayer=ios-mobileweb` , il server di manifesto restituisce l&#39;URL del manifesto master/variante in un oggetto JSON e il client invia una richiesta GET a tale URL del manifesto di variante.

1. Il client sceglie un flusso nel manifesto di variante generato per la riproduzione, inviando informazioni di annuncio al server del manifesto.
1. Il server manifesto trasmette le informazioni fornite dal client al server di annunci e riceve gli annunci e gli URL di tracciamento annunci dal server di annunci. Se un annuncio fornito non è in formato HLS, il server manifesto lo invia a CRS per la conversione a HLS.
1. Il server manifesto blocca gli annunci nel manifesto del contenuto e invia il nuovo manifesto cucito al client.
1. Il client riproduce il contenuto con gli annunci cuciti ed effettua richieste agli URL di tracciamento specificati nei momenti specificati.

L&#39;inserimento di annunci Primetime supporta i client su molte piattaforme di distribuzione video. Non tutti i client sono basati sul pacchetto TVSDK Primetime, ma tutti i client inviano richieste GET allo stesso URL di base. I parametri di query distinguono una richiesta client da un&#39;altra indicando al server manifesto:

* quale cliente sta effettuando la richiesta,
* cosa vuole quel cliente,
* e quali informazioni sul tracciamento degli annunci fornire.

## CORS {#section_BEA7F298660944BE92801E4C82FCD038}

Il server manifesto utilizza lo standard CORS (Cross-Origin Resource Sharing). Cerca un&#39; `Origin` intestazione nelle richieste ricevute. Se l&#39;intestazione è presente, risponde con

* `Access-Control-Allow-Origin: *`stringa dall&#39;intestazione Origin`*`
* `Access-Control-Allow-Credentials: true`
* `Access-Control-Allow-Methods: GET`

In caso contrario, risponde con:

* `Access-Control-Allow-Origin: *`
* `Access-Control-Allow-Methods: GET`