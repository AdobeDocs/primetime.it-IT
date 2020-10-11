---
title: Integrare la rete CDN
description: Integrazione della rete CDN
translation-type: tm+mt
source-git-commit: 7d74e526dbc4c9f623d1ec30e4bc70d9318a89f9
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 0%

---


# Integrare la rete CDN {#integrating-cdn}

Primetime  Ad Insertion funge da proxy tra l&#39;applicazione client e i manifesti, non i blocchi video stessi. Distribuite il contenuto alla rete CDN desiderata e passate l&#39;URL al Ad Insertion  Primetime utilizzando l&#39;API di Bootstrap.<!-- For integration details, see [Supported CDNs](supported-cdns.md).-->

## Schemi di token CDN supportati {#cdn-tokenization-schemes}

Le CDN dispongono spesso di diversi schemi di token per l’autorizzazione dei frammenti. Primetime  Ad Insertion supporta in modo nativo le principali reti CDN, tra cui:

* Akamai
* Limelight
* Centurylink / Livello3
* Per un elenco completo dei CDN supportati, contattate il rappresentante di supporto Primetime

Per ulteriori informazioni sul `pttoken` parametro, consultate [Bootstrap descrizione](/help/dynamic-ad-insertion/msapi-topics/ms-getting-started/ms-api-query-params.md)parametro API.

## Configurare gli annunci da distribuire dalla rete CDN del contenuto {#configure-ad-deliver-from-cdn}

Potreste desiderare di distribuire annunci e contenuti dalla stessa CDN per mantenere l&#39;affinità dei contenuti, aiutare a bypassare i blocchi di annunci e/o ottimizzare il numero di connessioni richieste dall&#39;applicazione client. Primetime  Ad Insertion supporta le regole di riscrittura dei frammenti per mappare i frammenti sulla rete CDN del contenuto.

<!--## Increase start-up performance with your CDN {#increase-startup-performance}

For more information, see [Optimizing start-up](optimize-video-startup-time.md).-->

## Funzioni multi-CDN {#enable-multi-cdn-fetures}

Contattate il rappresentante del supporto Primetime per abilitare le funzioni multi-CDN.
