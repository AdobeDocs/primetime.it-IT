---
description: Il CRS fornisce un pacchetto JIT (Just-in-time) e asincrono e la conversione HLS-to-HLS. Il risultato della ricompilazione è una versione HLS formattata dell'annuncio pubblicitario originale. CRS posiziona la versione formattata HLS sul server CDN (content delivery network, rete di distribuzione dei contenuti) per l'utilizzo quando necessario.
seo-description: Il CRS fornisce un pacchetto JIT (Just-in-time) e asincrono e la conversione HLS-to-HLS. Il risultato della ricompilazione è una versione HLS formattata dell'annuncio pubblicitario originale. CRS posiziona la versione formattata HLS sul server CDN (content delivery network, rete di distribuzione dei contenuti) per l'utilizzo quando necessario.
seo-title: Principali utilizzi del CRS
title: Principali utilizzi del CRS
uuid: df2caa67-bc94-4146-9b93-14edc060c3d5
translation-type: tm+mt
source-git-commit: e1e33d3ac0aad44859cd49566331524da72ac7e4
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---


# Principali utilizzi di CRS {#main-uses-of-crs}

Il CRS fornisce un pacchetto JIT (Just-in-time) e asincrono e la conversione HLS-to-HLS. Il risultato della ricompilazione è una versione HLS formattata dell&#39;annuncio pubblicitario originale. CRS posiziona la versione formattata HLS sul server CDN (content delivery network, rete di distribuzione dei contenuti) per l&#39;utilizzo quando necessario.

In JIT, il reimballaggio  Adobe Primetime e l&#39;inserimento degli annunci inizia il processo di ricompilazione quando incontra per la prima volta un annuncio pubblicitario non HLS. Ciò comporta in genere la perdita di opportunità di eseguire l&#39;annuncio durante il processo di reimballaggio.

Nella ricompilazione asincrona, l&#39;annuncio creativo viene transcodificato e memorizzato prima che sia necessario, il che può eliminare quelle opportunità perdute.

Nella conversione HLS-a-HLS, il CRS riformatta un annuncio HLS creativo in blocchi di dimensioni appropriate per garantire una riproduzione coerente.

## Reimballaggio in tempo reale {#section_1BA344F2300B49F291865A7461EDFEAE}

La sequenza per il reimballaggio JIT è la seguente:

1. Il server del manifesto recupera un annuncio.
1. Se il formato dell&#39;annuncio è HLS, il server manifesto inserisce l&#39;annuncio nel flusso di contenuto.
1. Se il formato non è HLS (ad esempio, MP4, FLV o WebM), il server manifesto cerca una versione transcodificata sul server CDN. Se ne trova uno, inserisce l&#39;annuncio transcodificato nel flusso di contenuto.
1. Se il formato non è HLS e il server CDN non dispone di una versione transcodificata, il server manifesto trasmette l’annuncio a CRS, che transcodifica l’annuncio creativo e memorizza il risultato sul server CDN per un utilizzo successivo.
1. Il server manifesto restituisce il contenuto senza l’annuncio.

## Reimballaggio asincrono {#section_ACDFB43FDA4B445CB9F2A107FEB4F2F7}

Potete utilizzare l&#39;API descritta in [Repackage API](../~old-creative-repackaging-service/api-repackage.md) per precodificare un creativo non HLS al fine di ridurre al minimo la perdita di impression e massimizzare la monetizzazione.

## Conversione HLS-in-HLS {#section_877A0E7E8FAF4C2DB086A31C24D53435}

Per evitare il buffering e il ritardo, un client scarica un video in piccoli blocchi. Se le dimensioni dei blocchi non sono coerenti, la riproduzione potrebbe risultare instabile. La conversione da HLS a HLS assicura che i blocchi di dati abbiano tutti la stessa durata (ad esempio, 6 secondi).

>[!NOTE]
>
>CRS produce la versione HLS 3, indipendentemente dalla versione HLS ricevuta.