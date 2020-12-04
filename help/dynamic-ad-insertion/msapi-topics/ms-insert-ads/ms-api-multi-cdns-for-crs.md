---
description: Mentre lo scenario predefinito del servizio di reimballaggio creativo (CRS) prevede l’utilizzo di una rete CDN (Content Delivery Network), potete distribuire le risorse CRS su più CDN.
seo-description: Mentre lo scenario predefinito del servizio di reimballaggio creativo (CRS) prevede l’utilizzo di una rete CDN (Content Delivery Network), potete distribuire le risorse CRS su più CDN.
seo-title: Supporto CDN multiplo per la distribuzione di annunci CRS
title: Supporto CDN multiplo per la distribuzione di annunci CRS
uuid: c5557a38-aa49-4161-bb58-3e8dff9a4d64
translation-type: tm+mt
source-git-commit: f327b45de7e482dcb25407659846b2098f1fd49d
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 0%

---


# Supporto CDN multiplo per la distribuzione di annunci CRS {#multiple-cdn-support-for-crs-ad-delivery}

Mentre lo scenario predefinito del servizio di reimballaggio creativo (CRS) prevede l’utilizzo di una rete CDN (Content Delivery Network), potete distribuire le risorse CRS su più CDN.

## Requisiti

Potete usare più CDN per i seguenti motivi:

* Requisiti per la scalabilità per eventi di visualizzazione di grandi dimensioni
* Requisito per far corrispondere l’origine CDN della risorsa CRS all’origine CDN del contenuto principale.
* Un requisito per utilizzare un CDN diverso da quello predefinito del CRS (Akamai).

Quando il server manifesto effettua una ricerca per le richieste transcodificate, utilizza un URL di avvio che contiene una serie di parametri di query. Se avete impostato un ambiente multi-CDN, anche l&#39;URL di avvio dovrà contenere il parametro `ptcdn`. Il server manifesto utilizza questo parametro per identificare il server CDN da cui ottenere la versione transcodificata dell’annuncio.

Per ulteriori dettagli, consultare [Supporto multi CDN](../../creative-repackaging-service/multi-cdn-supportt.md) nella documentazione CRS.
