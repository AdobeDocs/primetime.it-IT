---
title: Integrare la rete CDN
description: Integrazione della rete CDN
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---

# Integrare la rete CDN {#integrating-cdn}

Primetime Ad Insertion funge da proxy tra l’applicazione client e i manifesti, non i blocchi video stessi. Distribuisci il contenuto su CDN desiderato e passa l’URL all’Ad Insertion di Primetime utilizzando l’API Bootstrap. Per informazioni dettagliate sull’integrazione, consulta [CDN supportati](/help/primetime-ad-insertion/technical-reference/supported-cdns.md).

## Schemi di tokenizzazione CDN supportati {#cdn-tokenization-schemes}

Le CDN spesso presentano diversi schemi di tokenizzazione per l’autorizzazione dei frammenti. Primetime Ad Insertion supporta in modo nativo le principali reti CDN, tra cui:

* Akamai
* Limelight
* Centurylink/Livello3
* Per un elenco completo dei CDN supportati, contatta il rappresentante del supporto Primetime

Per ulteriori informazioni su `pttoken` parametro, vedi [Bootstrap descrizione parametro API](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md#parameter-description).

## Configurare gli annunci da distribuire dalla rete CDN dei contenuti {#configure-ad-deliver-from-cdn}

Puoi distribuire annunci e contenuti dalla stessa rete CDN per mantenere l’affinità tra i contenuti, evitare gli ad blocker e/o ottimizzare il numero di connessioni richieste dall’applicazione client. Primetime Ad Insertion supporta le regole di riscrittura dei frammenti per mappare i frammenti sulla rete CDN del contenuto. Per ulteriori informazioni, consulta [Riscrittura del manifesto](/help/primetime-ad-insertion/technical-reference/manifest-rewriting.md).

## Aumentare le prestazioni di avvio con la rete CDN {#increase-startup-performance}

Per ulteriori informazioni, consulta [Ottimizzazione dell’avvio](/help/primetime-ad-insertion/best-practices/optimize-video-startup-time.md).

## Funzioni multi-CDN {#enable-multi-cdn-fetures}

Contatta il rappresentante del supporto Primetime per abilitare le funzioni multi-CDN.
