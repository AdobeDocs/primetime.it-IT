---
title: Note sulla versione di PTAI 20.3.3
description: Le note sulla versione di PTAI 20.3.3 descrivono le novità o le modifiche, i problemi risolti e noti in Primetime Dynamic Ad Insertion nel 2020.
translation-type: tm+mt
source-git-commit: ededb36a0b460fff4644a3716b36971ff9454c37

---


# Note sulla versione Primetime Dynamic Ad Insertion 20.3.3

Le note sulla versione Dynamic Ad Insertion 20.3.3 descrivono le novità o le modifiche apportate, i problemi risolti e noti in Primetime Dynamic Ad Insertion nel 2020.

## Novità di PTAI 20.3.3

**Quando:** Giovedì 26 marzo 2020 dalle 03:00 alle 04:00 a Est

* Le risposte SSAI 4XX e 5XX ora forniscono correttamente le intestazioni relative a CORS, consentendo ai client javascript/webview di leggere con successo le risposte agli errori tra domini.

* È stato risolto un problema con le intestazioni X-Forwarded-For, a causa del quale gli indirizzi IPv6 non venivano codificati correttamente nell&#39;URL quando venivano passati ai server degli annunci.

* È stato risolto un problema con i flussi audio CMAF/demuxed, a causa del quale in alcuni scenari i numeri EXT-X-MEDIA-SEQUENCE aumentavano in modo errato

## Modifiche apportate alle versioni precedenti

### Versione

**Quando:**

### Versione

**Quando:**

## Problemi risolti

Se la risoluzione è associata a un problema segnalato, viene visualizzato un riferimento Zendesk. Ad esempio, ZD#xxxxx.

**PTAI 20.3.3**

* Problema con le intestazioni X-Forwarded-For, per cui gli indirizzi IPv6 non venivano codificati correttamente nell&#39;URL quando venivano passati ai server degli annunci.

* Problema con i flussi audio CMAF/demuxed, dove in alcuni scenari i numeri EXT-X-MEDIA-SEQUENCE aumentano in modo errato in alcuni scenari

## Problemi noti e limitazioni

**PTAI 20.3.3**

Nessuna nuova limitazione aggiunta.
