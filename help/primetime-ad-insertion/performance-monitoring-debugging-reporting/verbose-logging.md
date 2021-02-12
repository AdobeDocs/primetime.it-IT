---
title: Registrazione dettagliata
description: null
translation-type: tm+mt
source-git-commit: d5e948992d7c59e80b530c8f4619adbffc3c03d8
workflow-type: tm+mt
source-wordcount: '2155'
ht-degree: 0%

---


# Registrazione dettagliata {#verbose-logging}

## descrizioni dell&#39;evento ptdebug/logging {#ptdebug-logging-events}

Quando avviate la registrazione di debug per una sessione del server manifesto, potete aggiungere il parametro `ptdebug` all&#39;URL della richiesta per specificare le seguenti opzioni per le informazioni restituite dal server manifesto nelle intestazioni HTTP:

* `ptdebug=true`
Tutti i record eccetto TRACE_HTTP_HEADER e la maggior parte dei dati di chiamata/risposta dai record TRACE_AD_CALL.

* `ptdebug=AdCall`
Solo record TRACE_AD_ (ad esempio, TRACE_AD_CALL).

* `ptdebug=Header`
Solo record TRACE_HTTP_HEADER.

## Formati dei record di registro {#log-record-formats}

Ogni record di registro ha un tipo e un set di campi, alcuni dei quali potrebbero essere facoltativi. I campi di tutti i record fino al tipo di record sono gli stessi. Forniscono una marca temporale e informazioni sulla sessione. Il tipo di record identifica il tipo di evento da registrare e i campi successivi forniscono informazioni sull&#39;evento registrato.

La struttura di un record di registro è la seguente:

`datetime request_id session_id zone_id record_type other fields`.

| Field | Tipo | Descrizione |
|---|---|---|
| datetime | string | Timestamp |
| request_id | string | ID richiesta utilizzato dal server manifesto (marca temporale Unix) |
| session_id | string | ID sessione utilizzato dal server manifesto |
| zone_id | integer | Zona |
| record_type | string | Tipo di evento da registrare |
| altri campi | variation | Dipende dal tipo di evento |

I record di questo tipo registrano i risultati delle richieste HTTP. I campi oltre `TRACE_REQUEST_INFO` vengono visualizzati nell&#39;ordine indicato nella tabella, separati da tabulazioni.

| Field | Tipo | Descrizione |
|---|---|---|
| status | string | Codice di stato HTTP restituito |
| request_method | string | Metodo HTTP (GET o POST) |
| request_uri | string | URI richiesta HTTP (senza host) |
| request_length | integer | Lunghezza della richiesta (byte) |
| response_length | integer | Lunghezza della risposta (byte) |
| delta | integer | Tempo (millisecondi) per elaborare la richiesta |
| module_type | string | Variante, Flusso o VOD |
| remote_address_aud_client_ip | string | **mso** |
| remote_address_x_fwd_for_hdr_key | string | **mso** |
| remote_host_port | string | **mso** |

**†** Gli ultimi tre campi sono facoltativi.

**Un esempio**

```shell
1427263800524 6495aafc-3f34-4047-ad36-350d4f056eb4 189938TRACE_REQUEST_INFO 301 GET /auditude/variant/pubAsset/aHR0cDov. . ..m3u8?u=cecebae72a919de350b9ac52602623f3&z=189938&ptcueformat=turner& sid =yk-cnnlive-003 &ptdebug=true 0 0 0 Variant 111.22.3.44 111.22.3.45 127.0.0.1:46383
```

### Record TRACE_HTTP_HEADER {#trace-http-header-records}

Record di questo tipo di intestazioni HTTP del registro scambiate durante le chiamate HTTP tra il server manifesto e il client, il server di annunci o il server del contenuto. I campi oltre TRACE_HTTP_HEADER vengono visualizzati nell’ordine indicato nella tabella, separati da tabulazioni.

| Field | Tipo | Descrizione |
|---|---|---|
| request_type | string | Tipo di richiesta (PRINCIPALE o SCONOSCIUTA) |
| request_response | string | Intestazione risposta (richiesta o risposta) |
| header_name | string | Nome intestazione HTTP |
| header_value | string | Valore dell&#39;intestazione HTTP con codifica Base64 |

>[!NOTE]
>
>I campi `request_type` e `header_value` sono facoltativi.

**Un esempio**

```shell
2015-03-25T06:10:00.927Z 1427263800573 6495aa. . . 189938 TRACE_MISC Requesting: /cnn/tvecnn/stream4/stream_Layer.m3u8
2015-03-25T06:10:00.927Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN REQUEST Cookie aGRu. . .
2015-03-25T06:10:00.928Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN REQUEST User-Agent TW96aW. . .
2015-03-25T06:10:01.063Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Server bmd4X2. . .
2015-03-25T06:10:01.063Z  1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Content-Type YXBwb. . .
2015-03-25T06:10:01.063Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Last-Modified V2VkL. . .
2015-03-25T06:10:01.063Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE ETag IjIyY2. . .
2015-03-25T06:10:01.063Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Vary QWNjZXB. . .
2015-03-25T06:10:01.063Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Cache-Control bWF4LW. . .
2015-03-25T06:10:01.064Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Expires V2VkL. . .
2015-03-25T06:10:01.064Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Date V2VkLCA. . .
2015-03-25T06:10:01.064Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Age MQ==
2015-03-25T06:10:01.064Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Via MS4xIH. . .
```

### TRACE_AD_CALL record {#tracing-ad-call-records}

I record di questo tipo registrano i risultati delle richieste di annunci server manifest. I campi oltre `TRACE_AD_CALL` vengono visualizzati nell&#39;ordine indicato nella tabella, separati da tabulazioni.

| Field | Tipo | Descrizione |
|---|---|---|
| status | string | Codice di stato HTTP restituito |
| request_Duration | integer | Tempo (millisecondi) dalla richiesta alla risposta |
| ad_server_query_url | string | URL per la chiamata di annuncio, inclusi i parametri di query |
| ad_system_id | string | Ad system, dalla risposta del server di annunci (Auditude se non specificato) |
| avail_id | string | ID del valore, dal cue point dell&#39;annuncio nel file manifesto del contenuto (N/D per VOD) |
| avail_Duration | number | Durata (secondi) del valore, dal cue point dell&#39;annuncio nel file manifesto del contenuto (N/D per VOD) |
| ad_server_response | string | Risposta con codifica Base64 dal server di annunci |

Esempio:

```shell
2015-03-25T06:13:31.271Z 14272. . . 189938 TRACE_AD_CALL200 8 https://ad.stg2.auditude.com/adserver/a?cip=0.0.0.0&g=1000012&of=1.5 &ptcueformat=turner&ptdebug=true&tl=l,150,30,m&tm=63&u=ceceb. . . Auditude IvpIyC. . . 150 PD94bWw. . .
```

### record TRACE_AD_INSERT, TRACE_AD_RESOLVE e TRACE_AD_REDIRECT {#trace-ad-insert-resolve-redirect}

I record di questo tipo registrano i risultati delle richieste di annunci indicate dal tipo di record. I campi oltre il tipo di record vengono visualizzati nell&#39;ordine indicato nella tabella, separati da tabulazioni.

| Field | Tipo | Descrizione |
|---|---|---|
| status | string | È stato restituito il codice di stato HTTP. |
| avail_id | string | ID del valore, dal cue point dell&#39;annuncio nel file manifesto del contenuto (live) o dal server manifesto (VOD). |
| ad_type | string | Tipo di annuncio (DIRECT o REDIRECT). |
| ad_Duration | integer | Durata (secondi) dell’annuncio, dalla risposta del server dell’annuncio. |
| ad_content_url | string | URL del file manifesto dell&#39;annuncio, dalla risposta del server dell&#39;annuncio. |
| **†** ad_content_url_effective | string | URL del file manifesto dell&#39;annuncio inserito. Vuoto per TRACE_AD_REDIRECT. |
| ad_system_id | string | Ad system, dalla risposta del server di annunci (Auditude se non specificato). |
| ad_id | string | ID dell&#39;annuncio, dalla risposta del server di annunci. |
| creative_id | string | ID del creativo, dal nodo dell&#39;annuncio, dalla risposta del server dell&#39;annuncio. |
| **†** ad_call_id | string | Non utilizzato. Riservato per uso futuro. |
| delta | integer | Tempo (millisecondi) impiegato da questo evento. |
| **†** misc | string | Ragione annuncio è stato saltato. |

**†** `ad_content_url_actual`,  `ad_call_id`e  `misc` i campi sono facoltativi.

>[!NOTE]
>
>Per `TRACE_AD_RESOLVE` e `TRACE_AD_INSERT`, l&#39;URL nel campo `ad_content_url_actual` è relativo all&#39;annuncio transcodificato, se disponibile. In caso contrario, il campo è vuoto per `TRACE_AD_RESOLVE` o equivale a `ad_content_url` per `TRACE_AD_INSERT`.

Esempio:

```shell
2015-03-18T22:25:36.229-07:00 1426742736208 1120feb. . . 147465 TRACE_AD_RESOLVE200 0 DIRECT 15 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8 Auditude 308008 0  cecebae72a919de350b9ac52602623f3 0 NA
2015-03-18T22:25:36.230-07:00 1426742736208 1120feb. . . 147465 TRACE_AD_RESOLVE200 2 DIRECT 15 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8 Auditude 308008 0  cecebae72a919de350b9ac52602623f3 0 NA
2015-03-18T22:25:36.562-07:00 1426742736208 1120feb. . . 147465 TRACE_AD_INSERT200 0 DIRECT 15 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8Auditude 308008 0 cecebae72a919de350b9ac52602623f3 0 NA
2015-03-18T22:25:36.563-07:00 1426742736208 1120feb. . . 147465 TRACE_AD_INSERT200 2 DIRECT 15 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8Auditude 308008 0 cecebae72a919de350b9ac52602623f3 0 NA
```

<!-- ### TRACE_TRACKING_URL records {#trace-tracking-url-records}

Records of this type log the results of manifest server ad requests. Fields beyond `TRACE_TRACKING_URL` appear in the order shown in the table, separated by tabs.

| Field | Type | Description |
|---|---|---|
| pts | number | Program timestamp. Time within video to call the URL. |
| ad_system | string | Ad system (auditude or freewheel) |
| url | string | URL pinged |
| status | string | HTTP status returned from the ping |

```shell
2015-06-04T23:24:42.000-0700 1426742736208 3086f5cd . . . 12345 TRACE_TRACKING_URL 0.000000 ExampleSystem https://localhost/index.php?stream:test#8.1433485415; sid:3086f5cd . . .;pts:0 200
```

-->

### TRACE_TRANSCODING_NO_MEDIA_TO_TRANSCODE record {#trace-transcoding-no-media-to-transcode}

I record di questo tipo registrano un annuncio creativo mancante. L&#39;unico campo oltre `TRACE_TRANSCODING_NO_MEDIA_TO_TRANSCODE` viene visualizzato nella tabella.

| Field | Tipo | Descrizione |
|---|---|---|
| ad_id | string | ID annuncio completo (FQ_AD_ID: Q_AD_ID\[;Q_AD_ID\[;Q_AD_ID...\] \] Q_AD_ID: PROTOCOLLO:AD_SYSTEM:AD_ID\[:CREATIVE_ID\[:MEDIA_ID\] \] PROTOCOLLO: AUDITUDE,VAST) |

I record di questo tipo registrano i risultati delle richieste di transcodifica inviate dal server manifesto a CRS. I campi oltre `TRACE_TRANSCODING_REQUESTED` vengono visualizzati nell&#39;ordine indicato nella tabella, separati da tabulazioni.

| Field | Tipo | Descrizione |
|---|---|---|
| ad_id | string | ID annuncio completo |
| ad_manifest_url | string | URL del file manifesto dell&#39;annuncio, dalla risposta del server dell&#39;annuncio |
| creative_type | string | Tipo di supporto |
| flag | string | ID3 indica se la richiesta di transcodifica include una richiesta per aggiungere un tag ID3 |
| target_Duration | string | Durata target (secondi) del creativo transcodificato |

I record di questo tipo indicano una richiesta di tracciamento lato server. I campi oltre `TRACE_TRACKING_REQUEST` vengono visualizzati nell&#39;ordine indicato nella tabella, separati da tabulazioni.

| Field | Tipo | Descrizione |
|---|---|---|
| tracking_url_count | integer | Numero di URL di tracciamento |
| start | float | Tempo di inizio del frammento PTS (secondi con precisione in millisecondi) |
| end | float | Tempo di fine del frammento PTS (secondi con precisione in millisecondi) |

I record di questo tipo forniscono un URL di tracciamento per il tracciamento lato server. I campi oltre `TRACE_TRACKING_REQUEST_URL` vengono visualizzati nell&#39;ordine indicato nella tabella, separati da tabulazioni.

| Field | Tipo | Descrizione |
|---|---|---|
| timestamp | float | Tempo (secondi, con precisione 0,001) nella sessione di riproduzione per il ping dell’URL di tracciamento. |
| ad_system | string | Ad system (ad esempio, auditude) |
| url | string | URL del ping |

Record di questo tipo di richieste di registro eseguite dal server manifesto per le didascalie `WEBVTT`. I campi oltre `TRACE_WEBVTT_REQUEST` vengono visualizzati nell&#39;ordine indicato nella tabella, separati da tabulazioni.

| Field | Tipo | Descrizione |
|---|---|---|
| status | string | Codice di stato HTTP restituito |
| vtt_uri | string | URL per richiesta |
| start | float | Ora inizio divisione (secondi con precisione in millisecondi) |
| end | float | Tempo di fine diviso (secondi con precisione in millisecondi) |

Record di questo tipo di risposte del registro inviate dal server manifesto ai client in `answer` alle richieste di didascalie `WEBVTT`. I campi oltre `TRACE_WEBVTT_RESPONSE` vengono visualizzati nell&#39;ordine indicato nella tabella, separati da tabulazioni.

| Field | Tipo | Descrizione |
|---|---|---|
| status | string | Codice di stato HTTP restituito |
| response | string | Risposta con codifica Base64 inviata al client |

Record di questo tipo di risposte del registro alle richieste del server manifesto per le didascalie `WEBVTT`. I campi oltre `TRACE_WEBVTT_SOURCE` vengono visualizzati nell&#39;ordine indicato nella tabella, separati da tabulazioni.

| Field | Tipo | Descrizione |
|---|---|---|
| status | string | Codice di stato HTTP restituito |
| source | string | Contenuto VTT originale con codifica Base64 |

I record di questo tipo consentono al server di manifesto di registrare eventi e informazioni non altrimenti pianificate per l&#39;acquisizione di annunci. Il campo oltre `TRACE_MISC` è costituito da una stringa di messaggio. I messaggi che potrebbero essere visualizzati includono:

* Annuncio ignorato: AdPlacement \[adManifestURL=https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . . .m3u8, durataSeconds=15.0, ignore=false, redirectAd=false, priorità=1\]
* AdPlacement adManifestURL= adManifestURL, durataSeconds= secondi, ignore= ignore, redirectAd= redirectAd, priority= priority
* La posizione dell&#39;annuncio ha restituito null.
* Annuncio bloccato.
* Chiamata annuncio non riuscita: messaggio di errore.
* Aggiunta di agente utente per recuperare il manifesto non elaborato: user-agent.
* Aggiunta di cookie per recuperare il manifesto non elaborato: #
* Messaggio di errore URL richiesto non valido. (Impossibile analizzare l&#39;URL della variante)
* URL denominato: URL ottenuto restituito: codice di risposta. (Live URL)
* URL denominato: Codice URL restituito: codice di risposta. (URL VOD)
* È stato rilevato un conflitto durante la risoluzione degli annunci: uno dei due elementi: inizio medio o fine medio-rollio rientra nel pre-rollio o prerotolo contenuto nel mid-roll (VOD).
* Rilevata eccezione non gestita generata dal gestore per URI: richiedi URL.
* Generazione del manifesto della variante completata. (Variante)
* Generazione del manifesto della variante completata.
* Eccezione nella gestione del reindirizzamento VAST *URL di reindirizzamento *errore: messaggio di errore.
* Impossibile recuperare la playlist dell&#39;annuncio per l&#39;URL del manifesto dell&#39;annuncio.
* Impossibile generare il manifesto di destinazione. (HLSManifestResolver)
* Impossibile analizzare la risposta della prima chiamata ad: messaggio di errore.
* Impossibile elaborare *GET|POST *richiesta percorso: richiedi URL. (Live/VOD)
* Impossibile elaborare la richiesta del manifesto live: richiedi URL. (Live)
* Impossibile restituire un manifesto di variante: messaggio di errore.
* Impossibile convalidare l&#39;ID gruppo: ID gruppo.
* Recupero del manifesto non elaborato: URL contenuto. (Live)
* Dopo il reindirizzamento VAST: reindirizzare l’URL.
* Trovate delle risorse vuote. (VOD)
* Trovati annunci *number*. (VOD)
* Richiesta HTTP ricevuta. (Primo messaggio)
* L&#39;annuncio viene ignorato perché la differenza tra la durata della risposta dell&#39;annuncio (*durata della risposta *sec) e la durata effettiva dell&#39;annuncio (*durata effettiva *sec) è maggiore del limite. (HLSManifestResolver)
* Ignorare un valore che non ha fornito alcun valore ID. (GroupAdResolver.java)
* Valore che ha fornito un valore di ora non valido ignorato: *tempo *per availId = ID valido.
* Il valore che ha fornito un valore di durata non valido viene ignorato: *durata *per availId = ID valido.
* Inizializza nuova sessione. (Variante)
* Metodo HTTP non valido. Deve essere un GET. (VOD)
* Metodo HTTP non valido. La richiesta di tracciamento deve essere un GET. (Live)
* Messaggio di errore URL richiesto non valido. (Variante)
* Gruppo non valido. (HLSManifestResolver)
* Richiesta non valida. Didascalia non è una richiesta di tracciamento valida. (VOD)
* Richiesta non valida. La richiesta di didascalia deve essere eseguita dopo che è stata stabilita la sessione. (VOD)
* Richiesta non valida. La richiesta di tracciamento deve essere eseguita dopo che è stata stabilita la sessione. (VOD)
* Istanza del server non valida per l&#39;ID del gruppo di sovraccarico: ID gruppo. (Live)
* Limite dei reindirizzamenti VAST raggiunti - numero.
* Chiamata ad annunci: ad call URL.
* Nessun manifesto trovato per: URL contenuto. (Live)
* Nessun valore corrispondente trovato per l&#39;ID valido: ID valido. (HLSManifestResolver)
* Nessuna sessione di riproduzione trovata. (HLSManifestResolver)
* Elaborazione della richiesta VOD per l&#39;URL del contenuto manifesto.
* Variante di elaborazione.
* Elaborazione della richiesta di didascalia per l&#39;URL del contenuto manifesto.
* Elaborazione della richiesta di tracciamento. (VOD)
* Reindirizza risposta annuncio vuota. (VASTStAX)
* Richiesta: URL.
* Risposta di errore di ritorno per la richiesta di GET perché non è stata trovata alcuna sessione di riproduzione. (VOD)
* Risposta di errore restituita per la richiesta di GET a causa di un errore interno del server.
* Risposta di errore di ritorno per la richiesta di GET che specifica una risorsa non valida: ID richiesta di annunci. (VOD)
* Risposta di errore di ritorno per la richiesta di GET che specifica un ID gruppo vuoto o non valido: ID gruppo. (VOD)
* Risposta di errore restituita per la richiesta di GET che specifica un valore di posizione di tracciamento non valido. (VOD)
* Risposta di errore di ritorno per la richiesta di GET con sintassi non valida - URL richiesta. (Live/VOD)
* Risposta di errore di ritorno per la richiesta con metodo HTTP non supportato: GET|POST. (Live/VOD)
* Restituzione del manifesto dalla cache. (VOD)
* Il server è sovraccarico. Procedete senza richiesta di punto e punto. (Variante)
* Iniziate a generare il manifesto di destinazione. (HLSManifestResolver)
* Avvia la generazione del manifesto della variante da: URL contenuto. (Variante)
* Iniziate a raggruppare gli annunci in manifest. (VODHLSResolver)
* Tentativo di cucire l&#39;annuncio su `HH:MM:SS`: AdPlacement \[adManifestURL= ad Manifest URL, durataSeconds= secondi, ignore= ignore, redirectAd= redirect ad, priority= priority.\] \(HLSManifestResolver\)
* Impossibile ottenere gli annunci a causa di una cronologia pitimeline non valida - ha restituito il contenuto senza annunci. (VOD)
* Impossibile ottenere gli annunci: è stato restituito il contenuto senza annunci. (VOD)
* Impossibile ottenere la richiesta di annuncio e non è stato fornito alcun URL di contenuto. (VOD)
* URL ricevuto valido. (VOD/Variant)
* Impossibile trovare la variante M3U8. (Variante)

### TRACE_PLAYBACK_PROGRESS record {#trace-playback-progress-records}

Il server manifesto genera record di questo tipo quando riceve un segnale sull’avanzamento della riproduzione durante il flusso di lavoro di tracciamento lato server. I campi oltre `TRACE_PLAYBACK_PROGRESS` vengono visualizzati nell&#39;ordine indicato nella tabella, separati da tabulazioni.

| Field | Tipo | Descrizione |
|---|---|---|
| status | string | Codice di stato HTTP |
| larghezza | integer | Larghezza di banda del flusso |
| pts | integer | Tempo PTS nel flusso |
| ms_time | integer | Ora in cui il server manifesto ha generato l’URL di tracciamento |
| url | string | URL di reindirizzamento |
| **intestazione** user_agent | string | Intestazione agente utente HTTP |
| **header_** dnt | integer | Intestazione non traccia HTTP |
| **** effective_remote_address | string | Indirizzo remoto IPv4 efficace |
| **remote_address** remote | string | Indirizzo remoto IPv4 |

**Gli** ultimi quattro campi sono facoltativi.

## Flussi bitrate multipli {#multiple-bitrate-streams}

Le richieste dei clienti per l&#39;inserimento di annunci in genere specificano più bitrate nella sequenza di riproduzione della variante in formato M3U8. Il server di manifesto genera e restituisce una nuova variante del file M3U8 contenente un collegamento M3U8 separato per ogni bitrate. Viene inoltre generato un ID gruppo univoco per collegare questi M3U8s.

Il server manifesto utilizza le informazioni contenute nella richiesta dell&#39;URL di Bootstrap del client per recuperare la playlist della variante di contenuto. Viene generata una nuova playlist di variante contenente collegamenti del server manifesto al contenuto a livello di flusso. Il client li utilizza per creare richieste di inserimento di annunci. I collegamenti del contenuto a livello di flusso del server manifesto hanno il formato seguente:

```shell
https://manifest.auditude.com/auditude/{live/vod}/{publisherAssetID}/{rendition}/
{groupID}/{base64-encoded url of the bit rate stream}.[m3u8]?{Query parameters}
```

* **live/**
vodIl server manifesto imposta questo valore in base al tipo di playlist del contenuto: Live/linear (
`#EXT-X-PLAYLIST-TYPE:EVENT`) o VOD (`#EXT-X-PLAYLIST-TYPE:VOD`)

* **ID univoco di**
publisherAssetIDPublisher per il contenuto specifico fornito nella richiesta di Bootstrap URL.

* ****
renditionIl server manifest imposta questo valore in base al 
`BANDWIDTH` il valore del flusso di contenuto e lo utilizza per far corrispondere il bitrate dell&#39;annuncio al bitrate del contenuto. Il bitrate dell&#39;annuncio non può superare il bitrate del contenuto a meno che la rappresentazione dell&#39;annuncio con il bitrate più basso non lo faccia.

* ****
groupIDTil server manifest genera questo valore e lo utilizza per garantire che gli annunci vengano inseriti in modo coerente, indipendentemente dal quale il valore di bitrate viene visualizzato dal client.

* **url con codifica base64 del**
flusso di bit rateIl server manifesto URL-safe base64 codifica l&#39;URL assoluto del flusso di contenuto. Ogni flusso ha un proprio URL.

* **Parametri**
queryParametri query forniti nella richiesta di Bootstrap URL.
