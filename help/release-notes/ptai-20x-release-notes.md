---
title: Note sulla versione di PTAI 20.6.1
description: Le note sulla versione di PTAI 20.6.1 descrivono le novità o le modifiche, i problemi risolti e noti in Primetime Dynamic Ad Insertion nel 2020.
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '667'
ht-degree: 0%

---


# Note sulla versione Primetime Dynamic Ad Insertion 20.6.1

Le note sulla versione Dynamic Ad Insertion 20.6.1 descrivono le novità o le modifiche apportate, i problemi risolti e noti in Primetime Dynamic Ad Insertion nel 2020.

## Novità di PTAI 20.6.1

**Quando:** Martedì 2 giugno 2020 dalle 03:00 alle 05:00 Ora orientale

**Nuove funzioni**

Contattate il supporto Adobe per abilitare le seguenti nuove funzionalità tramite la configurazione lato server:

* Manipolazione manifesto: Ora è possibile trasformare gli URL di segmenti e risorse HLS tra HTTP e HTTPS per migliorare le prestazioni riducendo i handshakes TLS sulle richieste back-end. Può essere utilizzato anche per unificare frammenti di annunci/contenuti nelle stesse CDN.

* VOD a forma lunga: Sono state migliorate le API per mantenere in vita le sessioni con risorse VOD lunghe.

**Correzioni dei bug**

* È stato risolto un problema per il quale i frammenti WebVTT venivano sempre richiesti in base al protocollo http, indipendentemente dal protocollo originale richiesto.

* È stato risolto un problema per il quale i tag EXT-X-DISCONTINUITY venivano rimossi dalla parte superiore della playlist quando si passava dagli annunci ai contenuti. Per abilitare questa correzione, contattate il supporto Adobe.

### Versione 20.5.1

**Quando:** Martedì 5 maggio 2020 dalle 04:00 alle 05:00 ora orientale

* È stato risolto un problema per garantire che le intestazioni CORS corrette vengano fornite quando vengono inviate le intestazioni If-Modified-Since.

* Correzioni di bug nel dashboard CRS.

* Aggiornamenti di manutenzione.

### Versione 20.3.4

**Quando:** Mercoledì, 1 aprile 2020 dalle 03:00 AM alle 04:00 AM Ora orientale

* È stato risolto un problema che causava la mancata sincronizzazione dei sottotitoli dopo l&#39;inserimento di annunci in VOD/WebVTT.

* Aggiornamenti di protezione.

### Versione 20.3.3

**Quando:** Giovedì 26 marzo 2020 dalle 03:00 AM alle 04:00 Ora orientale

* Le risposte SSAI 4XX e 5XX ora forniscono correttamente le intestazioni relative a CORS, consentendo ai client di visualizzazione Web javascript tra domini di leggere con successo le risposte agli errori.

* È stato risolto un problema con le intestazioni X-Forwarded-For, a causa del quale gli indirizzi IPv6 non venivano codificati correttamente nell&#39;URL quando venivano passati ai server degli annunci.

* È stato risolto un problema con i flussi audio CMAF/demuxed, a causa del quale in alcuni scenari i numeri EXT-X-MEDIA-SEQUENCE aumentavano in modo errato.

### Versione 20.3.2

**Quando:** Mercoledì 11 marzo 2020 dalle 05:30 AM alle 07:00 AM Ora orientale

* Miglioramenti alla gestione del segnale SCTE35.

* Aggiornamenti di manutenzione.

### Versione 20.3.1

**Quando:** Giovedì 05 marzo 2020 dalle 02:30 alle 04:30 Ora orientale

* Miglioramenti delle prestazioni:

   * È stato aggiunto il supporto della cache per i manifesti m3u8 master/media. Questi manifesti ora rispondono a Cache-Control: intestazioni public e Max-Age, che possono spesso migliorare le prestazioni di avvio video.

   * È stato aggiunto il supporto per forzare il recupero delle creatività https tramite http, che può anche migliorare le prestazioni di avvio video.

* Correzioni di sicurezza e manutenzione.

### Versione 20.2.1

**Quando:** Giovedì 13 febbraio 2020 dalle 04:30 alle 05:30 Ora orientale

* È stato aggiunto il supporto per l’unione di risorse pubblicitarie contenenti più flussi solo audio in base al linguaggio/codec/bitrate.
* Piccoli miglioramenti delle prestazioni e aggiornamenti di manutenzione.

### Versione 20.1.3

**Quando:** Martedì 28 gennaio 2020 dalle 2:00 alle 03:00 Ora orientale

* **VMAP con supporto FER per nbc CueFormat**

   Convertire segnali dal flusso FER in param di sostituzione della timeline FW, quando `ptcueformat=nbc` viene utilizzato e il flusso è un flusso VOD con segnali in-manifest e annunci al forno.

* Inserite il campo agente utente in Intestazione HTTP prima di inviarlo a fornitori di annunci/CDN di terze parti.

* Filtrare i caratteri di controllo/non stampabili (codice ASCII &lt; 32) dalle intestazioni HTTP dell&#39;agente utente prima di inviarli ad Auditude e ad altri fornitori di annunci, CDN. Auditude Ad-Call utilizzata per errore per tali intestazioni non valide.

* Rimuovere vecchi oggetti V1 dai gruppi NetStorage per mantenere il conteggio degli oggetti entro i limiti di sicurezza di Akamai.

### Versione 20.1.2 (Hotfix)

**Quando:** Lunedì 20 gennaio 2020 dalle 02:00 alle 03:00 ora orientale

* Aggiornamenti di manutenzione.

### Versione 20.1.1

**Quando:** Mercoledì 15 gennaio 2020 dalle 04:00 alle 05:00 Ora orientale

* Creative Repackaging Service offre ora un inserimento più rapido degli annunci tramite l&#39;inserimento automatico di un elenco di creativi malformati.

* È stato aggiunto il supporto per la fase 1 per il nuovo formato di cue SCTE 35 nell&#39;inserimento di annunci lato server.

* Aggiornamenti di manutenzione.

## Problemi risolti

Se la risoluzione è associata a un problema segnalato, viene visualizzato un riferimento Zendesk. Ad esempio: `ZD#xxxxx`

**PTAI 20.5.1**

* Problemi con le intestazioni CORS quando vengono inviate le intestazioni If-Modified-Since.

* Problemi nel dashboard CRS.

**PTAI 20.3.4**

* Problema che causava la mancata sincronizzazione dei sottotitoli dopo l’inserimento di annunci in VOD/WebVTT.

**PTAI 20.3.3**

* Problema con le intestazioni X-Forwarded-For, per cui gli indirizzi IPv6 non venivano codificati correttamente nell&#39;URL quando venivano passati ai server degli annunci.

* Problema con i flussi audio CMAF/demuxed, dove in alcuni scenari i numeri EXT-X-MEDIA-SEQUENCE aumentano in modo errato in alcuni scenari

## Problemi noti e limitazioni

**PTAI 20.3.3**

Nessuna nuova limitazione aggiunta.
