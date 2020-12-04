---
title: Note sulla versione di PTAI 20.10.1
description: Le note sulla versione di PTAI 20.10.1 descrivono le novità o le modifiche, i problemi risolti e noti in Primetime  Ad Insertion nel 2020.
translation-type: tm+mt
source-git-commit: 7d74e526dbc4c9f623d1ec30e4bc70d9318a89f9
workflow-type: tm+mt
source-wordcount: '1027'
ht-degree: 0%

---


# Note sulla versione di Primetime  Ad Insertion 20.10.1

Le note sulla versione di Primetime  Ad Insertion 20.10.1 descrivono le novità o le modifiche apportate, i problemi risolti e noti in Primetime  Ad Insertion nel 2020.

## Novità di PTAI 20.10.1

**Quando:** martedì 13 ottobre 2020 dalle 03:00 alle 07:00 ora orientale

**Modifiche**

* Aggiornamenti di manutenzione.

### Miglioramenti e correzioni nelle versioni precedenti

#### Versione 20.9.3

**Quando:** Mercoledì 30 Settembre 2020 alle 3:30 AM alle 6:30 Ora orientale

**Modifiche**

* È stato aggiunto il parametro API Bootstrap `ptparallelstream`. Questo consente ai clienti con lettori che richiedono flussi audio o video demussati CMAF in parallelo, per garantire che gli annunci nelle tracce audio e video siano coerenti. Impostate il valore del parametro su true per abilitare questa funzione o omettete di disattivarla.

#### Versione 20.9.2

**Quando:** martedì 15 settembre 2020 dalle 3:30 alle 6:30 ora orientale

**Miglioramenti**

* È stato fornito il supporto per l&#39;inclusione di tipi di annunci non lineari utilizzando i tag `EXT-X-MARKER`.
Per ulteriori informazioni o per attivare questa funzione, contattate il rappresentante di assistenza tecnica.

* È stato fornito il supporto necessario per limitare il tempo complessivo di risoluzione degli annunci, se i fornitori richiedono troppo tempo per rispondere. Per abilitare la limitazione, impostate il parametro API di avvio `ptadtimeout` su un valore in millisecondi.

   >[!NOTE]
   >
   >Questo timeout si applica solo alle richieste di annunci, non alle richieste di annunci creativi.

#### Versione 20.9.1

**Quando:** martedì 1 settembre 2020 dalle 3:30 alle 7:30 ora orientale

**Modifiche**

* È stato risolto il problema per i clienti che utilizzano HLS/CMAF, a causa del quale talvolta i token CDN o i tag EXT-X-MAP mancavano a volte nella finestra DVR.

#### Versione 20.8.4

**Quando:** mercoledì 19 agosto 2020 dalle 03:30 alle 07:30 Ora orientale

**Miglioramenti e correzioni**

Aggiornamenti di manutenzione.

#### Versione 20.8.1

**Quando:** Martedì 4 Agosto 2020 dalle 3:00 AM alle 6:00 Ora orientale

**Miglioramenti e correzioni**

Aggiornamenti di manutenzione.

#### Versione 20.7.1

**Quando:** giovedì 9 luglio 2020 dalle 03:00 alle 05:00 ora orientale

**Nuove funzioni e miglioramenti**

* Miglioramento di SCTE35 per l&#39;utilizzo di messaggi di inizio/fine annuncio fornitore o di inizio/fine interruzione per identificare il cue point.

* Intestazione X-ADBE-AI-X1 aggiornata con informazioni aggiuntive per la risoluzione dei problemi.

* Aggregazione delle metriche migliorata.

* Pannello Console SSAI ottimizzato per il pannello Stati sessione

#### Versione 20.6.2

**Quando:** giovedì 18 giugno 2020 dalle 03:00 alle 04:00 ora orientale

**Miglioramenti**

Migliorata la sincronizzazione del flusso per i client video che richiedono una precisione in millisecondi. Contattate  Adobe Support per abilitare la precisione in millisecondi per `#EXT-X-PROGRAM-DATE-TIME tags`.

#### Versione 20.6.1

**Quando:** martedì 2 giugno 2020 dalle 03:00 alle 05:00 ora orientale

**Nuove funzioni**

Contattate il supporto  Adobe per abilitare le seguenti nuove funzionalità tramite la configurazione lato server:

* Manipolazione manifesto: Ora è possibile trasformare gli URL di segmenti e risorse HLS tra HTTP e HTTPS per migliorare le prestazioni riducendo i handshakes TLS sulle richieste back-end. Può essere utilizzato anche per unificare frammenti di annunci/contenuti nelle stesse CDN.

* VOD a forma lunga: Sono state migliorate le API per mantenere in vita le sessioni con risorse VOD lunghe.

**Correzioni di bug**

* È stato risolto un problema per il quale i frammenti WebVTT venivano sempre richiesti in base al protocollo http, indipendentemente dal protocollo originale richiesto.

* È stato risolto un problema per il quale i tag EXT-X-DISCONTINUITY venivano rimossi dalla parte superiore della playlist quando si passava dagli annunci ai contenuti. Per abilitare questa correzione, contattate  Adobe.

#### Versione 20.5.1

**Quando:** martedì 5 maggio 2020 dalle 04:00 alle 05:00 ora orientale

* È stato risolto un problema per garantire che le intestazioni CORS corrette vengano fornite quando vengono inviate le intestazioni If-Modified-Since.

* Correzioni di bug nel dashboard CRS.

* Aggiornamenti di manutenzione.

#### Versione 20.3.4

**Quando:** mercoledì 1 aprile 2020 dalle 03:00 alle 04:00 ora orientale

* È stato risolto un problema che causava la mancata sincronizzazione dei sottotitoli dopo l&#39;inserimento di annunci in VOD/WebVTT.

* Aggiornamenti di protezione.

#### Versione 20.3.3

**Quando:** giovedì 26 marzo 2020 dalle 03:00 alle 04:00 ora orientale

* Le risposte SSAI 4XX e 5XX ora forniscono correttamente le intestazioni relative a CORS, consentendo ai client di visualizzazione Web javascript tra domini di leggere con successo le risposte agli errori.

* È stato risolto un problema con le intestazioni X-Forwarded-For, a causa del quale gli indirizzi IPv6 non venivano codificati correttamente nell&#39;URL quando venivano passati ai server degli annunci.

* È stato risolto un problema con i flussi audio CMAF/demuxed, a causa del quale in alcuni scenari i numeri EXT-X-MEDIA-SEQUENCE aumentavano in modo errato.

#### Versione 20.3.2

**Quando:** mercoledì 11 marzo 2020 dalle 05:30 alle 07:00 ora orientale

* Miglioramenti alla gestione del segnale SCTE35.

* Aggiornamenti di manutenzione.

#### Versione 20.3.1

**Quando:** Giovedì 05 marzo 2020 dalle 02:30 alle 04:30 Ora orientale

* Miglioramenti delle prestazioni:

   * È stato aggiunto il supporto della cache per i manifesti m3u8 master/media. Questi manifesti ora rispondono a Cache-Control: intestazioni public e Max-Age, che possono spesso migliorare le prestazioni di avvio video.

   * È stato aggiunto il supporto per forzare il recupero delle creatività https tramite http, che può anche migliorare le prestazioni di avvio video.

* Correzioni di sicurezza e manutenzione.

#### Versione 20.2.1

**Quando:** Giovedì 13 febbraio 2020 dalle 04:30 alle 05:30 Ora orientale

* È stato aggiunto il supporto per l’unione di risorse pubblicitarie contenenti più flussi solo audio in base al linguaggio/codec/bitrate.
* Piccoli miglioramenti delle prestazioni e aggiornamenti di manutenzione.

#### Versione 20.1.3

**Quando:** martedì 28 gennaio 2020 dalle 2:00 alle 03:00 ora orientale

* **VMAP con supporto FER per nbc CueFormat**

   Convertire segnali dal flusso FER in param di sostituzione della timeline FW, quando si utilizza `ptcueformat=nbc` e il flusso è un flusso VOD con segnali in-manifest e annunci al forno.

* Inserite il campo agente utente in Intestazione HTTP prima di inviarlo a fornitori di annunci/CDN di terze parti.

* Filtrare i caratteri di controllo/non stampabili (codice ASCII &lt; 32) dalle intestazioni HTTP dell&#39;agente utente prima di inviarli ad Auditude e ad altri fornitori di annunci, CDN. Auditude Ad-Call utilizzata per errore per tali intestazioni non valide.

* Rimuovere vecchi oggetti V1 dai gruppi NetStorage per mantenere il conteggio degli oggetti entro i limiti di sicurezza di Akamai.

#### Versione 20.1.2 (Hotfix)

**Quando:** lunedì, 20 gennaio 2020 dalle 02:00 alle 03:00 Ora orientale

* Aggiornamenti di manutenzione.

#### Versione 20.1.1

**Quando:** mercoledì 15 gennaio 2020 dalle 04:00 alle 05:00 ora orientale

* Creative Repackaging Service offre ora un inserimento più rapido degli annunci tramite l&#39;inserimento automatico di un elenco di creativi malformati.

* È stato aggiunto il supporto per la fase 1 per il nuovo formato di cue SCTE 35 nell&#39;inserimento di annunci lato server.

* Aggiornamenti di manutenzione.

## Problemi risolti {#Resolved-issues}

Se la risoluzione è associata a un problema segnalato, viene visualizzato un riferimento Zendesk. Ad esempio, `ZD#xxxxx`.

**PTAI 20.9.1**

* È stato risolto il problema per i clienti che utilizzano HLS/CMAF, a causa del quale talvolta i token CDN o i tag EXT-X-MAP mancavano a volte nella finestra DVR.

**PTAI 20.6.1**

* `WebVTT` i frammenti sono sempre stati richiesti in base al protocollo http, indipendentemente dal protocollo originale richiesto.

* `EXT-X-DISCONTINUITY` i tag vengono rimossi dalla parte superiore della playlist quando si passa dagli annunci ai contenuti. Per abilitare questa correzione, contattate  Adobe.

**PTAI 20.5.1**

* Problemi con le intestazioni CORS quando vengono inviate le intestazioni If-Modified-Since.

* Problemi nel dashboard CRS.

**PTAI 20.3.4**

* Problema che causava la mancata sincronizzazione dei sottotitoli dopo l’inserimento di annunci in VOD/WebVTT.

**PTAI 20.3.3**

* Problema con le intestazioni X-Forwarded-For, per cui gli indirizzi IPv6 non venivano codificati correttamente nell&#39;URL quando venivano passati ai server degli annunci.

* Problema con i flussi audio CMAF/demuxed, dove in alcuni scenari i numeri EXT-X-MEDIA-SEQUENCE aumentano in modo errato in alcuni scenari

## Problemi noti e limitazioni

**PTAI 20.10.1**

Nessuna nuova limitazione aggiunta.
