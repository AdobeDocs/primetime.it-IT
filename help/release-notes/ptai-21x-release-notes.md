---
title: Note sulla versione di PTAI 21.11.1
description: Le note sulla versione PTAI descrivono le novità o le modifiche, i problemi risolti e noti in Primetime Ad Insertion nel 2021.
exl-id: 39a05f6d-431a-4416-81b1-21d82c0dbd69
source-git-commit: f4c6ef44c7f13bf8170a1f23a7ae8eba0171316a
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Note sulla versione di Primetime Ad Insertion 21.11.1

Le note sulla versione di Primetime Ad Insertion 21.xx.x descrivono le novità o le modifiche, i problemi risolti e i problemi noti in Primetime Ad Insertion nel 2021.

## Novità in PTAI 21.11.1

Quando: Martedì 9 novembre 2021 dalle ore 1:30 alle 04:30 ora orientale

* [!UICONTROL EXT-X-IMAGE-STREAM-INF] è ora configurabile per zona.

* Roku Trick Play è completamente supportato.

## Miglioramenti e correzioni nelle versioni precedenti

### Versione 21.10.1

Quando: Martedì 12 ottobre 2021 dalle 7:45 alle 13:45 ora orientale

* Server consolidati, server non di produzione rimossi e server non utili.

### Versione di manutenzione di Primetime Ad Insertion

Quando: Martedì 28 settembre 2021 dalle 5:00 alle 6:00 Ora orientale

* Aggiornamenti allo stack Load Balancer da AWS Elastic Load Balancer a AWS Application Load Balancer per funzionalità e scalabilità migliorate. Questi load balancer vengono utilizzati per indirizzare e richiedere il traffico al backend Auditude dal livello Ad Insertion (SSAI/CSAI).

### Versione 21.9.1

Quando: Martedì 7 settembre 2021 dalle 02:30 alle 05:30 Ora orientale

* Aggiornamenti ai componenti dell’infrastruttura alla base dei componenti per la mediazione e il reporting di Primetime Ad Insertion (GUI di Primetime Ads).

### Versione 21.8.1

Quando: Martedì 24 agosto 2021 dalle 2:00 alle 05:00 Ora orientale

* È stato aggiunto il supporto per i flussi DASH Live/ Linear (VOD è già supportato).

### Versione 21.5.1

Quando: Mercoledì 26 maggio 2021 dalle 3.30 alle 06.30 Ora orientale

**Modifiche**

* È stato aggiunto il supporto per il tipo di segmentazione obsoleta 0x01 (UPID) per i formati di cue basati su SCTE.

* È stata aggiunta una nuova telemetria per le prossime modifiche al dashboard.

### Versione 21.4.1

**Quando:** Giovedì 22 aprile 2021 dalle 2:00 alle 5:00 Ora orientale

**Modifiche**

* La limitazione della richiesta di sessione sarà abilitata per proteggere da potenziali attacchi DDOS. Le sessioni saranno limitate a 10 richieste al secondo, con un massimo di 100 richieste in coda. Non prevediamo alcun impatto sui giocatori che si comportano secondo le specifiche HLS/DASH.

* Altri miglioramenti a livello di manutenzione e sicurezza

### Versione 21.2.2

**Quando:** Martedì 23 febbraio 2021 dalle ore 1:00 alle 04:00 Ora orientale

**Modifiche**

* È stato aggiunto il supporto per l’inserimento/sincronizzazione del flusso EXT-X-IMAGE-STREAM-INF nei flussi HLS. La funzione viene abilitata tramite una configurazione lato server. Contatta il rappresentante del tuo account tecnico per abilitare la funzione.

### Versione 21.2.1

**Quando:** Mercoledì 3 febbraio 2021 dalle ore 1:00 alle 04:00 Ora orientale

**Modifiche**

* È stato aggiunto il supporto per l’ottimizzazione dell’output DASH: consolidamento dei nodi basato sul tempo.

### Versione 21.1.2

**Quando:** Martedì 19 gennaio 2021 dalle 12:30 alle 08:30 Ora orientale

**Modifiche**

* Aggiornamento di manutenzione: Aggiornamento dei cluster memcache back-end di Primetime Ad Insertion.

### Versione 21.1.1

**Quando:** Mercoledì 13 gennaio 2021 dalle 01:00 alle 04:00 Ora orientale

**Modifiche**

* È stato aggiunto il supporto per le risorse affiliate per i formati cue basati su SCTE35.
