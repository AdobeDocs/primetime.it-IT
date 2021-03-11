---
description: È possibile specificare o ignorare le timeline per le interruzioni pubblicitarie nel contenuto VOD utilizzando un elenco formattato di segmenti di annunci e contenuti denominati pod.
title: Formato della timeline VOD
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---


# Formato della timeline VOD {#vod-timeline-format}

È possibile specificare o ignorare le timeline per le interruzioni pubblicitarie nel contenuto VOD utilizzando un elenco formattato di segmenti di annunci e contenuti denominati pod.

## Contenitori {#section_606E9456E25E41C8B8537A023DDD96CE}

Un pod è un’interruzione pubblicitaria o un segmento di contenuto. Una timeline è costituita da una sequenza di baccelli, separati da punto e virgola. Esistono i seguenti tipi di pod:

### Pausa annunci

```
B,duration,maximum_number_of_ads,position
```

La durata è in secondi, con precisione di 0,001 (millisecondi); il numero di annunci è un numero intero. La posizione è una delle seguenti:
* **n** Nessuno — nessun annuncio
* **p** Pre-roll — prima del contenuto
* **m** Mid-roll — all&#39;interno del contenuto
* **t** Post-roll — dopo il contenuto

Ad esempio, `B,60,2,p` rappresenta un&#39;interruzione di un minuto per un massimo di 2 annunci prima del contenuto.

### Segmento di contenuto - capitolo

```
C,duration,number_of_lots
```

La durata è in secondi, con precisione di 0,001 (millisecondi); il numero di lotti (sezioni di contenuto) è un numero intero. Ad esempio, `C,300,1` rappresenta una singola sezione di contenuto di cinque minuti.