---
title: Configurare il tracciamento degli annunci
description: Impostazione del tracciamento degli annunci
exl-id: b5ebad0f-4e20-456a-892d-4c981ab26e51
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 0%

---

# Configurare il tracciamento degli annunci {#ser-up-ad-tracking}

La maggior parte degli inserzionisti richiede informazioni su quando, per quanto tempo e con quale successo sono stati visualizzati i loro annunci. Primetime Ad Insertion supporta il tracciamento degli annunci lato client, lato server e ibrido per fornire flessibilità nella raccolta di queste informazioni.

## Tracciamento annunci lato client con VMAP/JSON {#client-side-ad-tracking-vmap-json}

Nel tracciamento degli annunci lato client, il server invia al client una struttura JSON, VMAP o nel manifesto che specifica gli eventi di tracciamento e gli URL insieme alla playlist unita agli annunci.

Per abilitare il tracciamento degli annunci lato client, specifica i seguenti parametri nella [API BOOTSTRAP](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md).

* `pttrackingmode=simple`

* `pttrackingversion={format version (vmap,v1,v2,v3)}`

>[!NOTE]
>
>Impostazione di `pttrackingmode=simple` La richiesta API di avvio iniziale restituirà una risposta JSON, anziché un documento HLS o DASH.

<!-- **Daniel to check. The specified file in this statement does not exist.** 
More information about `pttrackingmode`, `pttrackingversion` formats, can be found in [API Reference: Manifest server query parameters](manifest-server-query-parameters.md). -->

<!--Show examples of how to request a sidecar] -->

## Tracciamento annunci lato server {#server-side-ad-tracking}

Utilizzando questo metodo, i dati di tracciamento degli annunci vengono calcolati interamente sul lato server. Questa opzione è utile quando non è possibile aggiornare l’applicazione client. Tuttavia, il tracciamento degli annunci lato server potrebbe non corrispondere all’attività di riproduzione lato client. Ad esempio, il server considera un annuncio da riprodurre dopo la distribuzione dei segmenti, anche se l’utente finale non visualizza l’intero annuncio.

Per abilitare il tracciamento degli annunci lato server, specifica il seguente parametro in [API BOOTSTRAP](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md).

`pttrackingmode=sstm`

Consulta `pttrackingmode` sezioni di [API BOOTSTRAP](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md).

Tutti i beacon di tracciamento degli annunci vengono inviati con le seguenti intestazioni di richiesta HTTP:

* `X-Forwarded-For`
* `User-Agent`
* `X-Device-User-Agent`

Questi valori contengono l’agente utente client/player e l’indirizzo IP del client.

## Tracciamento annunci ibridi {#hybrid-ad-tracking}

Questo approccio è simile al tracciamento lato server, ma l’applicazione client richiede anche sidecar dall’Ad Insertion Primetime per informazioni dettagliate sul tracciamento. Il tracciamento ibrido degli annunci può fornire annunci non lineari, come sovrapposizioni e compagni, all’applicazione client, pur continuando a fare affidamento su Primetime Ad Insertion per inviare singoli URL di tracciamento degli annunci.
Per abilitare il tracciamento degli annunci ibridi, consulta `pttrackingmode` parametro in [API BOOTSTRAP](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md).
