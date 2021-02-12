---
description: Potete specificare o ignorare le timeline per le interruzioni di annunci nel contenuto VOD utilizzando un elenco formattato di segmenti di annunci e contenuti denominato contenitori.
seo-description: Potete specificare o ignorare le timeline per le interruzioni di annunci nel contenuto VOD utilizzando un elenco formattato di segmenti di annunci e contenuti denominato contenitori.
seo-title: Formato della timeline VOD
title: Formato della timeline VOD
uuid: 6daaf605-e5ee-48dc-a222-a5973b3d915a
translation-type: tm+mt
source-git-commit: e437f4143fb939f46d106c64efc391137c33fe17
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---


# Formato della timeline VOD {#vod-timeline-format}

Potete specificare o ignorare le timeline per le interruzioni di annunci nel contenuto VOD utilizzando un elenco formattato di segmenti di annunci e contenuti denominato contenitori.

## Contenitori {#section_606E9456E25E41C8B8537A023DDD96CE}

Un contenitore è un&#39;interruzione annuncio o un segmento di contenuto. Una timeline è costituita da una sequenza di contenitori, separati da punto e virgola. Esistono i seguenti tipi di contenitori:

### Annuncio

```
B,duration,maximum_number_of_ads,position
```

La durata è in secondi, con precisione di 0,001 (millisecondi); il numero di annunci è un numero intero. La posizione è una delle seguenti:
* **n** Nessuno — no ad
* **p** Pre-roll — prima del contenuto
* **m** Mid-roll — all&#39;interno del contenuto
* **t** Post-roll — dopo il contenuto

Ad esempio, `B,60,2,p` rappresenta un&#39;interruzione di un minuto per un massimo di 2 annunci prima del contenuto.

### Segmento di contenuto - capitolo

```
C,duration,number_of_lots
```

La durata è in secondi, con precisione di 0,001 (millisecondi); il numero di lotti (sezioni di contenuto) è un numero intero. Ad esempio, `C,300,1` rappresenta una singola sezione di contenuto di cinque minuti.