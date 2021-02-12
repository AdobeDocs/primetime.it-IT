---
title: Imposta tracciamento annunci
description: Impostazione del tracciamento degli annunci
translation-type: tm+mt
source-git-commit: d5e948992d7c59e80b530c8f4619adbffc3c03d8
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 0%

---


# Imposta Ad Tracking {#ser-up-ad-tracking}

La maggior parte degli inserzionisti richiede informazioni su quando, per quanto tempo e con quale successo sono stati visualizzati i loro annunci. Primetime  Ad Insertion supporta il monitoraggio degli annunci lato client, lato server e ibrido per fornire flessibilità nella raccolta di tali informazioni.

## Tracciamento annunci lato client con VMAP/JSON {#client-side-ad-tracking-vmap-json}

Nel tracciamento degli annunci lato client, il server invia al client una struttura JSON, VMAP o in-manifest specificando eventi di tracciamento e URL insieme alla playlist con punti annuncio.

Per abilitare il tracciamento degli annunci lato client, specifica i seguenti parametri nell&#39; [Bootstrap API](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md).

* `pttrackingmode=simple`

* `pttrackingversion={format version (vmap,v1,v2,v3)}`

>[!NOTE]
>
>Se si imposta `pttrackingmode=simple`, la richiesta API di avvio iniziale restituirà una risposta JSON anziché un documento HLS o DASH.

<!-- **Daniel to check. The specified file in this statement does not exist.** 
More information about `pttrackingmode`, `pttrackingversion` formats, can be found in [API Reference: Manifest server query parameters](manifest-server-query-parameters.md). -->

<!--Show examples of how to request a sidecar] -->

## Tracciamento annunci lato server {#server-side-ad-tracking}

Utilizzando questo metodo, i dati di tracciamento degli annunci vengono calcolati interamente sul lato server. Questo è utile quando l&#39;aggiornamento dell&#39;applicazione client non è fattibile. Tuttavia, il tracciamento degli annunci lato server potrebbe non corrispondere all&#39;attività di riproduzione lato client. Ad esempio, il server considera un annuncio da riprodurre dopo la distribuzione dei segmenti, anche se l’utente finale non visualizza l’intero annuncio.

Per abilitare il tracciamento degli annunci lato server, specifica il seguente parametro nell&#39; [Bootstrap API](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md).

`pttrackingmode=sstm`

Vedere `pttrackingmode` sezioni di [Bootstrap API](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md).

Tutti i beacon di tracciamento degli annunci vengono inviati con le seguenti intestazioni di richiesta HTTP:

* `X-Forwarded-For`
* `User-Agent`
* `X-Device-User-Agent`

Questi valori contengono l’indirizzo IP client/lettore e l’agente utente client.

## Tracciamento annunci ibrido {#hybrid-ad-tracking}

Questo approccio è simile al tracciamento lato server, ma l&#39;applicazione client richiede anche sidecar da Primetime  Ad Insertion per informazioni di tracciamento dettagliate. Il tracciamento ibrido degli annunci può distribuire annunci non lineari come sovrapposizioni e companion all&#39;applicazione client, affidandosi comunque a Primetime  Ad Insertion per inviare singoli URL di tracciamento degli annunci.
Per abilitare il tracciamento ibrido degli annunci, fai riferimento al parametro `pttrackingmode` nell&#39; [Bootstrap API](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md).
