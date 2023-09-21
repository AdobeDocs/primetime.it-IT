---
title: Note sulla versione di PTAI 20.12.1
description: Le note sulla versione PTAI descrivono le novità o le modifiche, i problemi risolti e noti in Primetime Ad Insertion nel 2020.
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '1081'
ht-degree: 0%

---

# Note sulla versione di Primetime Ad Insertion 20.12.1

Le note sulla versione di Primetime Ad Insertion 20.12.1 descrivono le novità o le modifiche, i problemi risolti e i problemi noti in Primetime Ad Insertion nel 2020.

## Novità di PTAI 20.12.1

**Quando:** Martedì 8 dicembre 2020 dalle 01:00 alle 04:00 Ora orientale

**Modifiche**

* Include hotfix per risolvere i problemi di connettività client intermittente (5xx) rilevati in Primetime Ad Insertion il 30 novembre 2020.

## Miglioramenti e correzioni nelle versioni precedenti di

### Versione 20.11.1

**Quando:** Giovedì 5 novembre 2020 dalle 02:00 alle 05:00 Ora orientale

**Modifiche**

* Aggiornamenti di manutenzione.

### Versione 20.10.2

**Quando:** Giovedì 29 ottobre 2020 dalle 12:01 alle 06:00 Ora orientale

**Modifiche**

* Aggiornamenti di manutenzione.

### Versione 20.10.1

**Quando:** Martedì 13 ottobre 2020 dalle 03:00 alle 07:00 Ora orientale

**Modifiche**

* Aggiornamenti di manutenzione.

### Versione 20.9.3

**Quando:** Mercoledì 30 settembre 2020 alle 03:30 alle 06:30 fuso orientale

**Modifiche**

* Aggiunto parametro API Bootstrap `ptparallelstream`. Questo consente ai clienti con lettori che richiedono flussi audio o video demussi CMAF in parallelo per garantire che gli annunci nelle tracce audio e video siano coerenti. Imposta il valore del parametro su true per abilitare questa funzione o ometti per disabilitarla.

### Versione 20.9.2

**Quando:** Martedì 15 settembre 2020 dalle 03:30 alle 06:30 Ora orientale

**Miglioramenti**

* Fornito supporto per l&#39;inclusione di tipi di annunci non lineari tramite `EXT-X-MARKER` tag.
Per ulteriori informazioni o per attivare questa funzione, contattare il rappresentante del supporto tecnico.

* Fornito supporto per limitare i tempi complessivi di risoluzione degli annunci, se i provider impiegano troppo tempo per rispondere. Per abilitare la limitazione, imposta il parametro API bootstrap `ptadtimeout` a un valore in millisecondi.

  >[!NOTE]
  >
  >Questo timeout si applica solo alle richieste di annunci, non alle richieste creative di annunci.

### Versione 20.9.1

**Quando:** Martedì 1 settembre 2020 dalle 03:30 alle 07:30 Ora orientale

**Modifiche**

* È stato risolto il problema per i clienti che utilizzano HLS/CMAF, a causa del quale a volte EXT-X-MAP non disponeva di token CDN o tag EXT-X-MAP e veniva quindi distribuito in modo errato dalla finestra DVR.

### Versione 20.8.4

**Quando:** Mercoledì 19 agosto 2020 dalle 03:30 alle 07:30 Ora orientale

**Miglioramenti e correzioni**

Aggiornamenti di manutenzione.

### Versione 20.8.1

**Quando:** Martedì 4 agosto 2020 dalle 03:00 alle 06:00 Ora orientale

**Miglioramenti e correzioni**

Aggiornamenti di manutenzione.

### Versione 20.7.1

**Quando:** Giovedì 9 luglio 2020 dalle 03:00 alle 05:00 Ora orientale

**Nuove funzioni e miglioramenti**

* Miglioramento di SCTE35 per utilizzare i messaggi di inizio/fine annuncio del provider o i messaggi di inizio/fine interruzione per identificare il punto di partenza.

* L’intestazione X-ADBE-AI-X1 è stata aggiornata con ulteriori informazioni per facilitare la risoluzione dei problemi.

* Aggregazione metriche migliorata.

* Dashboard della console SSAI migliorato per il pannello Statistiche sessione

### Versione 20.6.2

**Quando:** Giovedì 18 giugno 2020 dalle 03:00 alle 04:00 Ora orientale

**Miglioramenti**

È stata migliorata la sincronizzazione dei flussi per client video che richiedono una precisione di millisecondi. Contatta il supporto Adobe per abilitare la precisione in millisecondi per `#EXT-X-PROGRAM-DATE-TIME tags`.

### Versione 20.6.1

**Quando:** Martedì 2 giugno 2020 dalle 03:00 alle 05:00 Ora orientale

**Nuove funzioni**

Contatta il supporto Adobe per abilitare le seguenti nuove funzioni tramite la configurazione lato server:

* Manipolazione del manifesto: ora è possibile trasformare gli URL di segmenti e risorse HLS tra HTTP e HTTPS per migliorare le prestazioni riducendo gli handshake TLS sulle richieste back-end. Può essere utilizzato anche per unificare frammenti di annunci e/o contenuti sulle stesse CDN.

* VOD in formato lungo: API migliorate per mantenere in vita la sessione con risorse VOD in formato lungo.

**Correzioni di bug**

* È stato risolto un problema a causa del quale i frammenti WebVTT venivano sempre richiesti nel protocollo http indipendentemente dal protocollo originale richiesto.

* È stato risolto un problema che causava la rimozione dei tag EXT-X-DISCONTINUITY dalla parte superiore della playlist quando si tornava dagli annunci al contenuto. Per abilitare questa correzione, contatta il supporto Adobe.

### Versione 20.5.1

**Quando:** Martedì 5 maggio 2020 dalle 04:00 alle 05:00 Ora orientale

* È stato risolto un problema per garantire che vengano fornite le intestazioni CORS corrette quando vengono inviate le intestazioni If-Modified-Since.

* Correzioni di bug nel dashboard CRS.

* Aggiornamenti di manutenzione.

### Versione 20.3.4

**Quando:** Mercoledì 1 aprile 2020 dalle 03:00 alle 04:00 fuso orientale

* È stato risolto un problema che causava la mancata sincronizzazione dei sottotitoli dopo l’inserimento di annunci in VOD/WebVTT.

* Aggiornamenti di sicurezza.

### Versione 20.3.3

**Quando:** Giovedì 26 marzo 2020 dalle 03:00 alle 04:00 Ora orientale

* Le risposte SSAI 4XX e 5XX ora forniscono correttamente intestazioni relative a CORS, consentendo ai client javascript webview di diversi domini di leggere correttamente le risposte di errore.

* È stato risolto un problema relativo alle intestazioni X-Forwarded-For a causa del quale gli indirizzi IPv6 non venivano codificati correttamente nell’URL quando venivano passati agli ad server.

* È stato risolto un problema relativo ai flussi audio CMAF/demuxed a causa del quale in alcuni scenari i numeri EXT-X-MEDIA-SEQUENCE non venivano incrementati correttamente.

### Versione 20.3.2

**Quando:** Mercoledì 11 marzo 2020 dalle 05:30 alle 07:00 Ora orientale

* Miglioramenti alla gestione del segnale SCTE35.

* Aggiornamenti di manutenzione.

### Versione 20.3.1

**Quando:** Giovedì 5 marzo 2020 dalle 02:30 alle 04:30 Ora orientale

* Miglioramenti delle prestazioni:

   * È stato aggiunto il supporto della cache per entrambi i manifesti master/media m3u8. Questi manifesti ora rispondono alle intestazioni Cache-Control: public e Max-Age, che spesso possono migliorare le prestazioni di avvio del video.

   * È stato aggiunto il supporto per forzare il recupero delle creatività https tramite HTTP, che può anche migliorare le prestazioni di avvio del video.

* Correzioni di sicurezza e manutenzione.

### Versione 20.2.1

**Quando:** Giovedì 13 febbraio 2020 dalle 04:30 alle 05:30 Ora orientale

* È stato aggiunto il supporto per l’unione di risorse annuncio che contengono più flussi di solo audio basati su linguaggio/codec/bitrate.
* Miglioramenti minori delle prestazioni e aggiornamenti di manutenzione.

### Versione 20.1.3

**Quando:** Martedì 28 gennaio 2020 dalle 02:00 alle 03:00 Ora orientale

* **VMAP con supporto FER per nbc CueFormat**

  Converte i segnali dal flusso FER in parametri di override della timeline FW, quando `ptcueformat=nbc` viene utilizzato e il flusso è un flusso VOD con suggerimenti nel manifesto e annunci al forno.

* Proteggi il campo user-agent nell’intestazione HTTP prima di inoltrarlo a provider di annunci/CDN di terze parti.

* Escludi i caratteri di controllo/non stampabili (codice ASCII &lt; 32) dalle intestazioni HTTP dell’agente utente prima di inviarli all’Auditude e ad altri provider di annunci, CDN. L’Auditude Ad-Call non riusciva per intestazioni non valide.

* Rimuovere i vecchi oggetti V1 dai gruppi NetStorage per mantenere il conteggio degli oggetti entro i limiti sicuri di Akamai.

### Versione 20.1.2 (Hotfix)

**Quando:** Lunedì 20 gennaio 2020 dalle 02:00 alle 03:00 Ora orientale

* Aggiornamenti di manutenzione.

### Versione 20.1.1

**Quando:** Mercoledì 15 gennaio 2020 dalle 04:00 alle 05:00 Ora orientale

* Il servizio Creative Repackaging ora offre un inserimento più rapido degli annunci bloccando automaticamente l’inserimento di creativi in formato non valido nell’elenco.

* È stato aggiunto il supporto della fase 1 per il nuovo formato di cue SCTE 35 nell’inserimento di annunci lato server.

* Aggiornamenti di manutenzione.

## Problemi risolti {#Resolved-issues}

Se la risoluzione è associata a un problema segnalato, viene visualizzato un riferimento a Zendesk. Ad esempio: `ZD#xxxxx`.

**PTAI 20.9.1**

* È stato risolto il problema per i clienti che utilizzano HLS/CMAF, a causa del quale a volte EXT-X-MAP non disponeva di token CDN o tag EXT-X-MAP e veniva quindi distribuito in modo errato dalla finestra DVR.

**PTAI 20.6.1**

* `WebVTT` i frammenti sono sempre stati richiesti nel protocollo http indipendentemente dal protocollo originale richiesto.

* `EXT-X-DISCONTINUITY` I tag vengono rimossi dall’inizio della playlist quando si torna dagli annunci al contenuto. Per abilitare questa correzione, contatta il supporto Adobe.

**PTAI 20.5.1**

* Problemi con le intestazioni CORS quando vengono inviate le intestazioni If-Modified-Since.

* Problemi nel dashboard CRS.

**PTAI 20.3.4**

* Problema che causava la mancata sincronizzazione dei sottotitoli dopo l’inserimento dell’annuncio in VOD/WebVTT.

**PTAI 20.3.3**

* Problema con le intestazioni X-Forwarded-For, in cui gli indirizzi IPv6 non venivano codificati correttamente nell’URL quando venivano passati agli ad server.

* Problema con i flussi audio CMAF/demuxed, dove in alcuni scenari i numeri EXT-X-MEDIA-SEQUENCE non aumentano correttamente in alcuni scenari

## Problemi noti e limitazioni

**PTAI 20.10.1**

Non è stata aggiunta alcuna nuova limitazione.
