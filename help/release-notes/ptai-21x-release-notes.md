---
title: Note sulla versione di PTAI 21.11.1
description: Le note sulla versione PTAI descrivono le novità o le modifiche, i problemi risolti e noti in Primetime Ad Insertion nel 2021.
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 0%

---

# Note sulla versione di Primetime Ad Insertion 21.11.1

Le note sulla versione di Primetime Ad Insertion 21.xx.x descrivono le novità o le modifiche, i problemi risolti e i problemi noti in Primetime Ad Insertion nel 2021.

## Novità di PTAI 21.11.1

Quando: martedì 9 novembre 2021 dalle 01:30 alle 04:30 Ora orientale

* [!UICONTROL EXT-X-IMAGE-STREAM-INF] è ora configurabile per zona.

* Roku Trick Play è completamente supportato.

## Miglioramenti e correzioni nelle versioni precedenti di

### Versione 21.10.1

Quando: martedì 12 ottobre 2021 dalle 07:45 alle 13:45 fuso orientale

* Server consolidati, server non di produzione e non utili rimossi.

### Versione di manutenzione per Ad Insertion di Primetime

Quando: martedì 28 settembre 2021 dalle 05:00 alle 06:00 ora orientale

* Aggiornamenti allo stack del load balancer da Elastic Load Balancer di AWS a Application Load Balancer di AWS per funzionalità e scalabilità migliorate. Questi load balancer vengono utilizzati per indirizzare e richiedere il traffico al backend di Auditude dal livello Ad Insertion (SSAI/CSAI).

### Versione 21.9.1

Quando: martedì 7 settembre 2021 dalle 02:30 alle 05:30 Ora orientale

* Aggiornamenti ai componenti dell’infrastruttura alla base dei componenti di reporting e mediazione di Primetime Ad Insertion (interfaccia utente di Primetime Ads).

### Versione 21.8.1

Quando: martedì 24 agosto 2021 dalle 02:00 alle 05:00 ora orientale

* È stato aggiunto il supporto per flussi DASH Live/ lineari (VOD è già supportato).

### Versione 21.5.1

Quando: Mercoledì 26 maggio 2021 dalle 03:30 alle 06:30 Ora orientale

**Modifiche**

* È stato aggiunto il supporto per il tipo di segmentazione obsoleto 0x01 (UPID) per i formati di cue basati su SCTE.

* È stata aggiunta una nuova telemetria per le modifiche imminenti al dashboard.

### Versione 21.4.1

**Quando:** Giovedì 22 aprile 2021 dalle 02:00 alle 05:00 Ora orientale

**Modifiche**

* La limitazione della richiesta di sessione verrà abilitata per la protezione contro potenziali attacchi DDOS. Le sessioni saranno limitate a 10 richieste al secondo, con un massimo di 100 richieste in coda. Non prevediamo alcun impatto sui giocatori che si comportano secondo le specifiche HLS/DASH.

* Altri miglioramenti di manutenzione e sicurezza

### Versione 21.2.2

**Quando:** Martedì 23 febbraio 2021 dalle 01:00 alle 04:00 Ora orientale

**Modifiche**

* È stato aggiunto il supporto per l’inserimento/sincronizzazione di flussi EXT-X-IMAGE-STREAM-INF nei flussi HLS. La funzione viene abilitata tramite una configurazione lato server. Contatta il rappresentante del tuo account tecnico per abilitare questa funzione.

### Versione 21.2.1

**Quando:** Mercoledì 3 febbraio 2021 dalle 01:00 alle 04:00 Ora orientale

**Modifiche**

* È stato aggiunto il supporto per l’ottimizzazione dell’output DASH: consolidamento dei nodi basato sul tempo.

### Versione 21.1.2

**Quando:** Martedì 19 gennaio 2021 dalle 12:30 alle 08:30 Ora orientale

**Modifiche**

* Aggiornamento di manutenzione: aggiornamento dei cluster memcache back-end Ad Insertion di Primetime.

### Versione 21.1.1

**Quando:** Mercoledì 13 gennaio 2021 dalle 01:00 alle 04:00 Ora orientale

**Modifiche**

* È stato aggiunto il supporto per la disponibilità di affiliate per i formati cue basati su SCTE35.
