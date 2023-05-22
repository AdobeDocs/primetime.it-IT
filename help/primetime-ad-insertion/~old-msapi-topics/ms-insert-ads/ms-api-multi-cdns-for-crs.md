---
description: Anche se lo scenario predefinito del servizio di reimballaggio creativo (CRS) prevede l’utilizzo di una rete CDN (Content Delivery Network), puoi distribuire le risorse CRS su più di una rete CDN.
title: Supporto di più CDN per la distribuzione di annunci CRS
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---


# Supporto di più CDN per la distribuzione di annunci CRS {#multiple-cdn-support-for-crs-ad-delivery}

Anche se lo scenario predefinito del servizio di reimballaggio creativo (CRS) prevede l’utilizzo di una rete CDN (Content Delivery Network), puoi distribuire le risorse CRS su più di una rete CDN.

## Requisiti

Puoi utilizzare più CDN per i seguenti motivi:

* Necessità di aumentare la scalabilità per gli eventi di visualizzazione di grandi dimensioni
* Requisito per la corrispondenza tra l’origine CDN della risorsa CRS e l’origine CDN del contenuto principale.
* Requisito relativo all’utilizzo di una rete CDN diversa da quella predefinita di CRS (Akamai).

Quando il server manifest cerca le richieste transcodificate, utilizza un URL di bootstrap che contiene una serie di parametri di query. Se hai impostato un ambiente con più reti CDN, l’URL di avvio deve contenere anche `ptcdn` parametro. Il server manifesto utilizza questo parametro per identificare il server CDN da cui ottenere la versione transcodificata dell’annuncio.

Per ulteriori dettagli, consulta [Supporto di più reti CDN](../../~old-creative-repackaging-service/multi-cdn-supportt.md) nella documentazione CRS.
