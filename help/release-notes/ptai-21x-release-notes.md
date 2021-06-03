---
title: Note sulla versione di PTAI 21.5.1
description: Le note sulla versione PTAI descrivono le novità o le modifiche, i problemi risolti e noti in Primetime Ad Insertion nel 2021.
exl-id: 39a05f6d-431a-4416-81b1-21d82c0dbd69
source-git-commit: fe0f5f3399d2e2ab3e07713fbcd29ede47888d98
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---

# Note sulla versione di Primetime Ad Insertion 21.5.1

Le note sulla versione di Primetime Ad Insertion 21.x.x descrivono le novità o le modifiche, i problemi risolti e i problemi noti in Primetime Ad Insertion nel 2021.

## Novità in PTAI 21.5.1

Quando:  Mercoledì 26 maggio 2021 dalle 3.30 alle 06.30 Ora orientale

* È stato aggiunto il supporto per il tipo di segmentazione obsoleta 0x01 (UPID) per i formati di cue basati su SCTE.

* È stata aggiunta una nuova telemetria per le prossime modifiche al dashboard.

## Miglioramenti e correzioni nelle versioni precedenti

### Versione 21.4.1

**Quando:** giovedì 22 aprile 2021 dalle 2:00 alle 5:00 ora orientale

**Modifiche**

* La limitazione della richiesta di sessione sarà abilitata per proteggere da potenziali attacchi DDOS. Le sessioni saranno limitate a 10 richieste al secondo, con un massimo di 100 richieste in coda. Non prevediamo alcun impatto sui giocatori che si comportano secondo le specifiche HLS/DASH.

* Altri miglioramenti a livello di manutenzione e sicurezza

### Versione 21.2.2

**Quando:** martedì 23 febbraio 2021 dalle 1:00 alle 04:00 ora orientale

**Modifiche**

* È stato aggiunto il supporto per l’inserimento/sincronizzazione del flusso EXT-X-IMAGE-STREAM-INF nei flussi HLS. La funzione viene abilitata tramite una configurazione lato server. Contatta il rappresentante del tuo account tecnico per abilitare la funzione.

### Versione 21.2.1

**Quando:** Mercoledì 3 febbraio 2021 dalle 1:00 alle 04:00 Ora orientale

**Modifiche**

* È stato aggiunto il supporto per l’ottimizzazione dell’output DASH: consolidamento dei nodi basato sul tempo.

### Versione 21.1.2

**Quando:** martedì 19 gennaio 2021 dalle 12:30 alle 08:30 ora orientale

**Modifiche**

* Aggiornamento di manutenzione: Aggiornamento dei cluster memcache back-end di Primetime Ad Insertion.

### Versione 21.1.1

**Quando:** mercoledì 13 gennaio 2021 dalle 01:00 alle 04:00 ora orientale

**Modifiche**

* È stato aggiunto il supporto per le risorse affiliate per i formati cue basati su SCTE35.
