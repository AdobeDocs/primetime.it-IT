---
title: Note sulla versione di Adobe Concurrency Monitoring 2.9
description: Note sulla versione di Adobe Concurrency Monitoring 2.9
source-git-commit: ac0c15b951f305e29bb8fa0bd45aa2c53de6ad15
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 0%

---


# Note sulla versione di Monitoraggio concorrenza 2.9 {#rn-cm29}

Questa pagina descrive nuove funzioni, modifiche e problemi noti relativi a questa versione.

## Data di rilascio {#release-date}

03/14/2019


## Panoramica sulla versione {#release-overview}

* A partire da questa versione è stato introdotto un nuovo rapporto per comprendere l’utilizzo simultaneo: un istogramma per il livello di concorrenza, che mostra:

* il numero di utenti che hanno raggiunto ogni livello di concorrenza (ovvero quanti utenti hanno mai avuto 2 flussi simultanei, 3 flussi simultanei e così via) durante ogni intervallo di granularità
* la durata totale in minuti di ciascun livello di concorrenza (il valore medio può essere calcolato dividendo semplicemente questo valore per il conteggio di cui sopra)
* il numero totale di volte in cui gli utenti hanno riscontrato ciascun livello di concorrenza, per stimare l’impatto di una determinata regola in termini sia di utenti interessati che di esperienza utente aggregata Maggiori dettagli sono disponibili sul [Rapporti utilizzo](/help/concurrency-monitoring/cm-usage-reports.md) pagina.

È stata inoltre migliorata la protezione SQL injection e sono state aggiunte diverse correzioni di bug.

## Problemi noti {#known-issues}

Nessuno.
