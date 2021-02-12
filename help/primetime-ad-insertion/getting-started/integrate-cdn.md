---
title: Integrare la rete CDN
description: Integrazione della rete CDN
translation-type: tm+mt
source-git-commit: d5e948992d7c59e80b530c8f4619adbffc3c03d8
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---


# Integrare la rete CDN {#integrating-cdn}

Primetime  Ad Insertion funge da proxy tra l&#39;applicazione client e i manifesti, non i blocchi video stessi. Distribuite il contenuto alla rete CDN desiderata e passate l&#39;URL al Ad Insertion  Primetime utilizzando l&#39;API di Bootstrap. Per informazioni dettagliate sull&#39;integrazione, consultate [CDN supportati](/help/primetime-ad-insertion/technical-reference/supported-cdns.md).

## Schemi di token CDN supportati {#cdn-tokenization-schemes}

Le CDN dispongono spesso di diversi schemi di token per l’autorizzazione dei frammenti. Primetime  Ad Insertion supporta in modo nativo le principali reti CDN, tra cui:

* Akamai
* Limelight
* Centurylink / Livello3
* Per un elenco completo dei CDN supportati, contattate il rappresentante di supporto Primetime

Per ulteriori informazioni sul parametro `pttoken`, vedere [Bootstrap descrizione parametro API](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md#parameter-description).

## Configurare gli annunci da distribuire dal contenuto CDN {#configure-ad-deliver-from-cdn}

Potreste desiderare di distribuire annunci e contenuti dalla stessa CDN per mantenere l&#39;affinità dei contenuti, aiutare a bypassare i blocchi di annunci e/o ottimizzare il numero di connessioni richieste dall&#39;applicazione client. Primetime  Ad Insertion supporta le regole di riscrittura dei frammenti per mappare i frammenti sulla rete CDN del contenuto. Per ulteriori informazioni, vedere [Riscrittura manifesto](/help/primetime-ad-insertion/technical-reference/manifest-rewriting.md).

## Aumentare le prestazioni di avvio con la rete CDN {#increase-startup-performance}

Per ulteriori informazioni, vedere [Ottimizzazione dell&#39;avvio](/help/primetime-ad-insertion/best-practices/optimize-video-startup-time.md).

## Funzioni multi-CDN {#enable-multi-cdn-fetures}

Contattate il rappresentante del supporto Primetime per abilitare le funzioni multi-CDN.
