---
description: CRS fornisce un pacchetto JIT (just-in-time) e asincrono e la conversione da HLS-a-HLS. Il risultato del riconfezionamento è una versione HLS formattata dell'annuncio originale creativo. CRS posiziona la versione formattata HLS sul server CDN (Content Delivery Network) per l’utilizzo quando necessario.
title: Principali utilizzi di CRS
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---


# Principali utilizzi di CRS {#main-uses-of-crs}

CRS fornisce un pacchetto JIT (just-in-time) e asincrono e la conversione da HLS-a-HLS. Il risultato del riconfezionamento è una versione HLS formattata dell&#39;annuncio originale creativo. CRS posiziona la versione formattata HLS sul server CDN (Content Delivery Network) per l’utilizzo quando necessario.

In JIT repackaging Adobe Primetime inserzione inizia il processo di riconfezionamento quando incontra per la prima volta un annuncio non-HLS creativo. Questo di solito comporta la perdita di opportunità di eseguire l&#39;annuncio durante il processo di riconfezionamento.

Nel repackaging asincrono, l’annuncio creativo viene codificato e memorizzato prima che sia necessario, il che può eliminare quelle opportunità perdute.

Nella conversione HLS-to-HLS, il CRS riformatta un annuncio HLS creativo in blocchi di dimensioni appropriate per garantire una riproduzione coerente.

## Repackaging just-in-time {#section_1BA344F2300B49F291865A7461EDFEAE}

La sequenza per il riconfezionamento JIT è la seguente:

1. Il server manifest recupera un annuncio.
1. Se il formato dell&#39;annuncio è HLS, il server manifesto inserisce l&#39;annuncio nel flusso di contenuto.
1. Se il formato non è HLS (ad esempio, MP4, FLV o WebM), il server manifesto cerca una versione transcodificata sul server CDN. Se ne trova uno, inserisce l’annuncio transcodificato nel flusso di contenuto.
1. Se il formato non è HLS e il server CDN non ha una versione transcodificata, il server manifest trasmette l&#39;annuncio a CRS, che transcodifica il creativo dell&#39;annuncio e memorizza il risultato sul server CDN per un uso successivo.
1. Il server manifest restituisce il contenuto senza l&#39;annuncio.

## Repackaging asincrono {#section_ACDFB43FDA4B445CB9F2A107FEB4F2F7}

Puoi utilizzare l&#39;API descritta in [Repackaging API](../~old-creative-repackaging-service/api-repackage.md) per precodificare un contenuto creativo non HLS per ridurre al minimo la perdita di impression e massimizzare la monetizzazione.

## Conversione da HLS a HLS {#section_877A0E7E8FAF4C2DB086A31C24D53435}

Per evitare buffering e ritardi, un client scarica un video in piccoli blocchi. Se le dimensioni dei blocchi sono incoerenti, la riproduzione potrebbe risultare instabile. La conversione da HLS a HLS assicura che i blocchi di dati abbiano la stessa durata (ad esempio, 6 secondi).

>[!NOTE]
>
>CRS produce HLS versione 3, indipendentemente dalla versione HLS che riceve.