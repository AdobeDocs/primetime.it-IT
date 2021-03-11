---
description: Mentre lo scenario predefinito del servizio di ricompilazione creativa (CRS) è quello di utilizzare una rete CDN (Content Delivery Network), puoi distribuire le risorse CRS su più di una rete CDN.
title: Supporto di più CDN per CRS e distribuzione di annunci
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---


# Supporto di più CDN per CRS e consegna di annunci {#multiple-cdn-support-for-crs-ad-delivery}

Mentre lo scenario predefinito del servizio di ricompilazione creativa (CRS) è quello di utilizzare una rete CDN (Content Delivery Network), puoi distribuire le risorse CRS su più di una rete CDN.

## Requisiti

Puoi utilizzare più CDN per i seguenti motivi:

* Un requisito per l&#39;ingrandimento di eventi di visualizzazione di grandi dimensioni
* Un requisito per far corrispondere l’origine CDN della risorsa CRS con l’origine CDN del contenuto principale.
* Un requisito per utilizzare una CDN diversa dalla CDN predefinita CRS (Akamai).

Quando il server manifest effettua una ricerca per le richieste transcodificate, utilizza un URL di bootstrap che contiene una serie di parametri di query. Se hai impostato un ambiente multi-CDN, anche l&#39;URL di avvio dovrà contenere il parametro `ptcdn` . Il server manifest utilizza questo parametro per identificare il server CDN da cui ottenere la versione transcodificata dell&#39;annuncio.

Per ulteriori dettagli, consulta [Supporto multi CDN](../../~old-creative-repackaging-service/multi-cdn-supportt.md) nella documentazione CRS.
