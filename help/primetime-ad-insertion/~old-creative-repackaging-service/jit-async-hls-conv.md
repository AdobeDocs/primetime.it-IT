---
description: CRS fornisce JIT (Just-In-Time) e il repackaging asincrono e la conversione da HLS a HLS. Il risultato del riconfezionamento è una versione formattata HLS della creatività dell’annuncio originale. CRS inserisce la versione formattata HLS sul server CDN (Content Delivery Network) per utilizzarla quando necessario.
title: Principali utilizzi di CRS
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---


# Principali utilizzi di CRS {#main-uses-of-crs}

CRS fornisce JIT (Just-In-Time) e il repackaging asincrono e la conversione da HLS a HLS. Il risultato del riconfezionamento è una versione formattata HLS della creatività dell’annuncio originale. CRS inserisce la versione formattata HLS sul server CDN (Content Delivery Network) per utilizzarla quando necessario.

Nel JIT, il repackaging degli annunci Adobe Primetime inizia il processo di repackaging quando incontra per la prima volta un annuncio creativo non HLS. Questo di solito comporta la perdita di opportunità di eseguire l’annuncio durante il processo di riconfezionamento.

In caso di riconfezionamento asincrono, la creatività dell’annuncio viene transcodificata e memorizzata prima che sia necessaria, eliminando in tal modo le opportunità perse.

Nella conversione da HLS a HLS, CRS riformatta un annuncio e un contenuto creativo HLS in blocchi di dimensioni appropriate per garantire una riproduzione coerente.

## Riconfezionamento rapido {#section_1BA344F2300B49F291865A7461EDFEAE}

La sequenza per il repackaging JIT è la seguente:

1. Il server manifesto recupera un annuncio.
1. Se il formato dell’annuncio è HLS, il server di manifesto inserisce l’annuncio nel flusso di contenuto.
1. Se il formato non è HLS (ad esempio, MP4, FLV o WebM), il server manifest cerca una versione transcodificata sul server CDN. Se ne trova uno, inserisce l’annuncio transcodificato nel flusso di contenuto.
1. Se il formato non è HLS e il server CDN non ha una versione transcodificata, il server manifesto trasmette l’annuncio a CRS, che transcodifica la creatività dell’annuncio e memorizza il risultato sul server CDN per un uso successivo.
1. Il server di manifesto restituisce il contenuto senza l’annuncio.

## Reimballaggio asincrono {#section_ACDFB43FDA4B445CB9F2A107FEB4F2F7}

Puoi utilizzare l’API descritta in [Riconfezionamento API](../~old-creative-repackaging-service/api-repackage.md) pre-trascodificare una creatività non HLS per ridurre al minimo la perdita di impression e massimizzare la monetizzazione.

## Conversione da HLS a HLS {#section_877A0E7E8FAF4C2DB086A31C24D53435}

Per evitare il buffering e il ritardo, un client scarica un video in piccoli blocchi. Se le dimensioni dei blocchi non sono coerenti, la riproduzione potrebbe essere a scatti. La conversione da HLS a HLS garantisce che i blocchi di dati abbiano tutti la stessa durata (ad esempio, 6 secondi).

>[!NOTE]
>
>CRS produce la versione 3 di HLS, indipendentemente dalla versione HLS ricevuta.