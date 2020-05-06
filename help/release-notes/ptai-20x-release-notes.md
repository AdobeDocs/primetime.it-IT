---
title: Note di rilascio di PTAI 20.5.1
description: Le note sulla versione di PTAI 20.5.1 descrivono le novità o le modifiche, i problemi risolti e noti in Primetime Dynamic Ad Insertion nel 2020.
translation-type: tm+mt
source-git-commit: 266b884707e9160d539a06fd089732ef8ade21ba
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 0%

---


# Note sulla versione Primetime Dynamic Ad Insertion 20.5.1

Le note sulla versione Dynamic Ad Insertion 20.5.1 descrivono le novità o le modifiche apportate, i problemi risolti e noti in Primetime Dynamic Ad Insertion nel 2020.

## Novità di PTAI 20.5.1

**Quando:** Martedì 5 maggio 2020 dalle 04:00 alle 05:00 AM EST

* È stato risolto un problema per garantire che le intestazioni CORS corrette vengano fornite quando vengono inviate le intestazioni If-Modified-Since.

* Correzioni di bug nel dashboard CRS.

* Aggiornamenti di manutenzione.

## Modifiche apportate alle versioni precedenti

### Versione 20.3.4

**Quando:** Mercoledì 1 aprile 2020 dalle 03:00 alle 04:00 AM EST

* È stato risolto un problema che causava la mancata sincronizzazione dei sottotitoli dopo l&#39;inserimento di annunci in VOD/WebVTT.

* Aggiornamenti di protezione.

### Versione 20.3.3

**Quando:** Giovedì 26 marzo 2020 dalle 03:00 alle 04:00 a Est

* Le risposte SSAI 4XX e 5XX ora forniscono correttamente le intestazioni relative a CORS, consentendo ai client javascript/webview di leggere con successo le risposte agli errori tra domini.

* È stato risolto un problema con le intestazioni X-Forwarded-For, a causa del quale gli indirizzi IPv6 non venivano codificati correttamente nell&#39;URL quando venivano passati ai server degli annunci.

* È stato risolto un problema con i flussi audio CMAF/demuxed, a causa del quale in alcuni scenari i numeri EXT-X-MEDIA-SEQUENCE aumentavano in modo errato.

### Versione 20.1.3

**Quando:** Martedì 28 gennaio 2020 dalle 2:00 alle 03:00 a Est

* **VMAP con supporto FER per nbc CueFormat**

   Convertire segnali dal flusso FER in param di sostituzione della timeline FW, quando `ptcueformat=nbc` viene utilizzato e il flusso è un flusso VOD con segnali in-manifest e annunci al forno.

* Inserite il campo agente utente in Intestazione HTTP prima di inviarlo a fornitori di annunci/CDN di terze parti.

* Filtrare i caratteri di controllo/non stampabili (codice ASCII &lt; 32) dalle intestazioni HTTP dell&#39;agente utente prima di inviarli ad Auditude e ad altri fornitori di annunci, CDN. Auditude Ad-Call utilizzata per errore per tali intestazioni non valide.

* Rimuovere vecchi oggetti V1 dai gruppi NetStorage per mantenere il conteggio degli oggetti entro i limiti di sicurezza di Akamai.

## Problemi risolti

Se la risoluzione è associata a un problema segnalato, viene visualizzato un riferimento Zendesk. Ad esempio, ZD#xxxxx.

**PTAI 20.3.3**

* Problema con le intestazioni X-Forwarded-For, per cui gli indirizzi IPv6 non venivano codificati correttamente nell&#39;URL quando venivano passati ai server degli annunci.

* Problema con i flussi audio CMAF/demuxed, dove in alcuni scenari i numeri EXT-X-MEDIA-SEQUENCE aumentano in modo errato in alcuni scenari

## Problemi noti e limitazioni

**PTAI 20.3.3**

Nessuna nuova limitazione aggiunta.
