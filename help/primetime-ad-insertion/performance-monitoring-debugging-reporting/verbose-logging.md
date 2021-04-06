---
title: Registrazione dettagliata
description: Registrazione dettagliata
copied-description: true
exl-id: f2d1b0c2-ba28-4fba-9a4e-71d1421f37fe
translation-type: tm+mt
source-git-commit: 3e63c187f12d1bff53370bbcde4d6a77f58f3b4f
workflow-type: tm+mt
source-wordcount: '2157'
ht-degree: 0%

---

# Registrazione dettagliata {#verbose-logging}

## descrizioni dell&#39;evento ptdebug/logging {#ptdebug-logging-events}

Quando si avvia la registrazione di debug per una sessione del server manifest, è possibile aggiungere il parametro `ptdebug` all&#39;URL della richiesta per specificare le seguenti opzioni per le informazioni restituite dal server manifest nelle intestazioni HTTP:

* `ptdebug=true`
Tutti i record ad eccezione di TRACE_HTTP_HEADER e della maggior parte dei dati di chiamata/risposta provenienti dai record TRACE_AD_CALL.

* `ptdebug=AdCall`
Solo record di tipo TRACE_AD_ (ad esempio, TRACE_AD_CALL).

* `ptdebug=Header`
Solo record TRACE_HTTP_HEADER.

## Formati dei record di log {#log-record-formats}

Ogni record di registro ha un tipo e un set di campi, alcuni dei quali potrebbero essere facoltativi. I campi di tutti i record fino al tipo di record sono gli stessi. Forniscono una marca temporale e informazioni sulla sessione. Il tipo di record identifica il tipo di evento registrato e i campi successivi forniscono informazioni sull’evento registrato.

La struttura di un record di log è la seguente:

`datetime request_id session_id zone_id record_type other fields`.

| Campo | Tipo | Descrizione |
|---|---|---|
| datetime | string | Timestamp |
| request_id | string | ID richiesta utilizzato dal server manifesto (timestamp Unix) |
| session_id | string | ID sessione utilizzato dal server manifest |
| zone_id | integer | Zona |
| record_type | string | Tipo di evento registrato |
| altri campi | varia | Dipende dal tipo di evento |

I record di questo tipo registrano i risultati delle richieste HTTP. I campi oltre `TRACE_REQUEST_INFO` vengono visualizzati nell’ordine indicato nella tabella, separati da tabulazioni.

| Campo | Tipo | Descrizione |
|---|---|---|
| status | string | Codice di stato HTTP restituito |
| request_method | string | metodo HTTP (GET o POST) |
| request_uri | string | URI di richiesta HTTP (senza host) |
| request_length | integer | Lunghezza della richiesta (byte) |
| response_length | integer | Lunghezza della risposta (byte) |
| delta | integer | Tempo (millisecondi) per elaborare la richiesta |
| module_type | string | Variant, Stream o VOD |
| remote_address_aud_client_ip | string | **infinito** |
| remote_address_x_fwd_for_hdr_key | string | **infinito** |
| remote_host_port | string | **infinito** |

**** Gli ultimi tre campi sono facoltativi.

**Un esempio**

```shell
1427263800524 6495aafc-3f34-4047-ad36-350d4f056eb4 189938TRACE_REQUEST_INFO 301 GET /auditude/variant/pubAsset/aHR0cDov. . ..m3u8?u=cecebae72a919de350b9ac52602623f3&z=189938&ptcueformat=turner& sid =yk-cnnlive-003 &ptdebug=true 0 0 0 Variant 111.22.3.44 111.22.3.45 127.0.0.1:46383
```

### Record TRACE_HTTP_HEADER {#trace-http-header-records}

Record di questo tipo di intestazioni HTTP log scambiate durante le chiamate HTTP tra il server manifesto e il client, ad server o server di contenuto. I campi che si trovano oltre TRACE_HTTP_HEADER vengono visualizzati nell’ordine indicato nella tabella, separati da tabulazioni.

| Campo | Tipo | Descrizione |
|---|---|---|
| request_type | string | Tipo di richiesta (PRINCIPALE o SCONOSCIUTO) |
| request_response | string | Intestazione della risposta (richiesta o risposta) |
| nome_intestazione | string | Nome intestazione HTTP |
| header_value | string | Valore di intestazione HTTP con codifica Base64 |

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

### Record TRACE_AD_CALL {#tracing-ad-call-records}

I record di questo tipo registrano i risultati delle richieste di annunci server manifest. I campi oltre `TRACE_AD_CALL` vengono visualizzati nell’ordine indicato nella tabella, separati da tabulazioni.

| Campo | Tipo | Descrizione |
|---|---|---|
| status | string | Codice di stato HTTP restituito |
| request_duration | integer | Tempo (millisecondi) dalla richiesta alla risposta |
| ad_server_query_url | string | URL per la chiamata dell’annuncio, inclusi i parametri di query |
| ad_system_id | string | Sistema di annunci, dalla risposta del server di annunci (Auditude se non specificato) |
| avail_id | string | ID del valore, dal cue dell’annuncio nel file manifesto del contenuto (N/D per VOD) |
| avail_duration | numero | Durata (secondi) del valore, dal cue dell&#39;annuncio nel file manifesto del contenuto (N/A per VOD) |
| ad_server_response | string | Risposta con codifica Base64 da ad server |

Esempio:

```shell
2015-03-25T06:13:31.271Z 14272. . . 189938 TRACE_AD_CALL200 8 https://ad.stg2.auditude.com/adserver/a?cip=0.0.0.0&g=1000012&of=1.5 &ptcueformat=turner&ptdebug=true&tl=l,150,30,m&tm=63&u=ceceb. . . Auditude IvpIyC. . . 150 PD94bWw. . .
```

### Record TRACE_AD_INSERT, TRACE_AD_RESOLVE e TRACE_AD_REDIRECT {#trace-ad-insert-resolve-redirect}

I record di questo tipo registrano i risultati delle richieste di annunci indicate dal tipo di record. I campi oltre il tipo di record vengono visualizzati nell’ordine indicato nella tabella, separati da tabulazioni.

| Campo | Tipo | Descrizione |
|---|---|---|
| status | string | Codice di stato HTTP restituito. |
| avail_id | string | ID del valore, dal cue dell’annuncio nel file manifesto del contenuto (live) o dal server manifesto (VOD). |
| ad_type | string | Tipo di annuncio (DIRETTO o REINDIRIZZATO). |
| ad_duration | integer | Durata (secondi) dell’annuncio, dalla risposta dell’ad server. |
| ad_content_url | string | URL del file manifesto dell&#39;annuncio, dalla risposta dell&#39;ad server. |
| **†** ad_content_url_real | string | URL del file manifesto dell&#39;annuncio inserito. Vuoto per TRACE_AD_REDIRECT. |
| ad_system_id | string | Sistema di annunci, dalla risposta del server di annunci (Auditude se non specificato). |
| ad_id | string | ID dell&#39;annuncio, dalla risposta dell&#39;ad server. |
| creative_id | string | ID del creativo, dal nodo dell&#39;annuncio, dalla risposta dell&#39;ad server. |
| **†** ad_call_id | string | Non utilizzato. Riservato per uso futuro. |
| delta | integer | Tempo (millisecondi) impiegato da questo evento. |
| **†** misc | string | Motivo ignorato. |

**†** `ad_content_url_actual`,  `ad_call_id` e  `misc` i campi sono facoltativi.

>[!NOTE]
>
>Per `TRACE_AD_RESOLVE` e `TRACE_AD_INSERT`, l’URL nel campo `ad_content_url_actual` è relativo all’annuncio transcodificato, se disponibile. In caso contrario, il campo è vuoto per `TRACE_AD_RESOLVE` o corrisponde a `ad_content_url` per `TRACE_AD_INSERT`.

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

### Record TRACE_TRANSCODING_NO_MEDIA_TO_TRANSCODE {#trace-transcoding-no-media-to-transcode}

Record di questo tipo registrano un annuncio creativo mancante. L’unico campo oltre `TRACE_TRANSCODING_NO_MEDIA_TO_TRANSCODE` viene visualizzato nella tabella.

| Campo | Tipo | Descrizione |
|---|---|---|
| ad_id | string | ID annuncio completo (FQ_AD_ID: Q_AD_ID\[;Q_AD_ID\[;Q_AD_ID..\] \] Q_AD_ID: PROTOCOLLO: AD_SYSTEM:AD_ID\[:CREATIVE_ID\[:MEDIA_ID\] \] PROTOCOLLO: AUDITUDE, VAST) |

I record di questo tipo registrano i risultati delle richieste di transcodifica inviate dal server manifest a CRS. I campi oltre `TRACE_TRANSCODING_REQUESTED` vengono visualizzati nell’ordine indicato nella tabella, separati da tabulazioni.

| Campo | Tipo | Descrizione |
|---|---|---|
| ad_id | string | ID annuncio completo |
| ad_manifest_url | string | URL del file manifesto dell&#39;annuncio, dalla risposta dell&#39;ad server |
| creative_type | string | Tipo di supporto |
| flag | string | ID3 indica se la richiesta di transcodifica include una richiesta per aggiungere un tag ID3 |
| target_duration | string | Durata del target (secondi) del contenuto creativo transcodificato |

I record di questo tipo indicano una richiesta per eseguire il tracciamento lato server. I campi oltre `TRACE_TRACKING_REQUEST` vengono visualizzati nell’ordine indicato nella tabella, separati da tabulazioni.

| Campo | Tipo | Descrizione |
|---|---|---|
| tracking_url_count | integer | Numero di URL di tracciamento |
| start | float | Tempo di avvio del frammento PTS (secondi con precisione in millisecondi) |
| end | float | Tempo di fine del frammento PTS (secondi con precisione in millisecondi) |

I record di questo tipo forniscono un URL di tracciamento per il tracciamento lato server. I campi oltre `TRACE_TRACKING_REQUEST_URL` vengono visualizzati nell’ordine indicato nella tabella, separati da tabulazioni.

| Campo | Tipo | Descrizione |
|---|---|---|
| timestamp | float | Tempo (secondi, con precisione .001) all’interno della sessione di riproduzione per eseguire il ping dell’URL di tracciamento. |
| ad_system | string | Sistema di annunci (ad esempio, auditude) |
| url | string | URL al ping |

Record di questo tipo di richieste di log effettuate dal server manifest per le didascalie `WEBVTT`. I campi oltre `TRACE_WEBVTT_REQUEST` vengono visualizzati nell’ordine indicato nella tabella, separati da tabulazioni.

| Campo | Tipo | Descrizione |
|---|---|---|
| status | string | Codice di stato HTTP restituito |
| vtt_uri | string | URL per la richiesta |
| start | float | Tempo di avvio diviso (secondi con precisione in millisecondi) |
| end | float | Tempo di fine diviso (secondi con precisione in millisecondi) |

Record di questo tipo di risposte al registro inviate dal server manifest ai client in `answer` alle richieste di didascalie `WEBVTT`. I campi oltre `TRACE_WEBVTT_RESPONSE` vengono visualizzati nell’ordine indicato nella tabella, separati da tabulazioni.

| Campo | Tipo | Descrizione |
|---|---|---|
| status | string | Codice di stato HTTP restituito |
| response | string | Risposta con codifica Base64 inviata al client |

Record di questo tipo di risposte di log alle richieste effettuate dal server manifest per le didascalie `WEBVTT`. I campi oltre `TRACE_WEBVTT_SOURCE` vengono visualizzati nell’ordine indicato nella tabella, separati da tabulazioni.

| Campo | Tipo | Descrizione |
|---|---|---|
| status | string | Codice di stato HTTP restituito |
| source | string | Contenuto VTT originale codificato in base64 |

I record di questo tipo consentono al server manifest di registrare eventi e informazioni non altrimenti pianificati per quando acquisisce annunci. Il campo oltre `TRACE_MISC` è costituito da una stringa di messaggio. I messaggi che potrebbero apparire includono:

* Annuncio ignorato: AdPlacement \[adManifestURL=https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . . .m3u8, durationSeconds=15.0, ignore=false, redirectAd=false, priority=1\]
* AdPlacement adManifestURL= adManifestURL, durationSeconds= secondi, ignore= ignore, redirectAd= redirectAd, priority= priority
* Il posizionamento dell&#39;annuncio ha restituito null.
* L&#39;annuncio è stato vincolato.
* Ad call non riuscita : messaggio di errore.
* Aggiunta di User-Agent per recuperare il manifesto non elaborato: agente utente.
* Aggiunta di cookie per recuperare il manifesto non elaborato: #
* Messaggio di errore URL richiesto non valido. (Impossibile analizzare l&#39;URL variante)
* URL chiamato: URL restituito: codice di risposta. ( URL live)
* URL chiamato: Codice di ritorno URL: codice di risposta. (URL VOD)
* È stato rilevato un conflitto durante la risoluzione degli annunci: uno di - inizio medio o fine medio-rollio rientra nel pre-roll o pre-roll contenuto nel mid-roll (VOD).
* Rilevata eccezione non gestita generata dal gestore per URI: URL della richiesta.
* Generazione del manifesto della variante completata. (Variant)
* Generazione del manifesto della variante completata.
* Eccezione nella gestione del reindirizzamento VAST *URL di reindirizzamento *errore: messaggio di errore.
* Impossibile recuperare la playlist dell&#39;annuncio per l&#39;URL del manifesto dell&#39;annuncio.
* Impossibile generare il manifesto di destinazione. (HLSManifestResolver)
* Impossibile analizzare la risposta della prima chiamata pubblicitaria: messaggio di errore.
* Impossibile elaborare *GET|POST *richiesta di percorso: URL della richiesta. (Live/VOD)
* Impossibile elaborare la richiesta del manifesto live: URL della richiesta. (Live)
* Impossibile restituire un manifesto variante: messaggio di errore.
* Impossibile convalidare l&#39;ID gruppo: ID gruppo.
* Recupero del manifesto non elaborato: URL contenuto. (Live)
* In seguito al reindirizzamento VAST: URL di reindirizzamento.
* Sono state trovate risorse vuote. (VOD)
* Trovati annunci *number*. (VOD)
* Richiesta HTTP ricevuta. (Messaggio molto primo)
* L&#39;annuncio viene ignorato perché la differenza tra la durata della risposta dell&#39;annuncio (*durata della risposta dell&#39;annuncio *sec) e la durata effettiva dell&#39;annuncio (*durata effettiva *sec) è maggiore del limite. (HLSManifestResolver)
* Valore che non ha fornito alcun valore ID ignorato. (GroupAdResolver.java)
* Valore che ha fornito un valore di ora non valido ignorato: *tempo *per availId = ID valido.
* Valore che ha fornito un valore di durata non valido ignorato: *durata *per availId = ID valido.
* Inizializza nuova sessione. (Variant)
* Metodo HTTP non valido. Deve essere un GET. (VOD)
* Metodo HTTP non valido. La richiesta di tracciamento deve essere un GET. (Live)
* Messaggio di errore URL richiesto non valido. (Variant)
* Gruppo non valido. (HLSManifestResolver)
* Richiesta non valida. La didascalia non è una richiesta di tracciamento valida. (VOD)
* Richiesta non valida. La richiesta di didascalia deve essere effettuata dopo che la sessione è stata stabilita. (VOD)
* Richiesta non valida. È necessario effettuare una richiesta di tracciamento dopo aver stabilito la sessione. (VOD)
* Istanza del server non valida per l&#39;ID del gruppo di sovraccarico: ID gruppo. (Live)
* Limite dei reindirizzamenti VAST raggiunti - numero.
* Effettuare una chiamata ad: URL di chiamata degli annunci.
* Nessun manifesto trovato per: URL contenuto. (Live)
* Nessun valore corrispondente trovato per un ID valido: ID valido. (HLSManifestResolver)
* Nessuna sessione di riproduzione trovata. (HLSManifestResolver)
* Elaborazione della richiesta VOD per l&#39;URL del contenuto manifesto.
* Variante di elaborazione.
* Elaborazione della richiesta di didascalia per l&#39;URL del contenuto manifesto.
* Elaborazione della richiesta di tracciamento. (VOD)
* Reindirizza risposta annuncio vuota. (VASTStAX)
* Richiesta: URL.
* Risposta di errore restituita per la richiesta GET perché non è stata trovata alcuna sessione di riproduzione. (VOD)
* Risposta di errore restituita per la richiesta GET a causa di un errore interno del server.
* Restituzione di una risposta di errore per la richiesta GET che specifica una risorsa non valida: ID richiesta annuncio. (VOD)
* Restituzione di una risposta di errore per la richiesta GET che specifica un ID gruppo non valido o vuoto: ID gruppo. (VOD)
* Restituzione di una risposta di errore per la richiesta GET che specifica un valore di posizione di tracciamento non valido. (VOD)
* Risposta di errore di ritorno per la richiesta GET con sintassi non valida - URL della richiesta. (Live/VOD)
* Risposta di errore di ritorno per la richiesta con metodo HTTP non supportato: GET|POST. (Live/VOD)
* Restituzione del manifesto dalla cache. (VOD)
* Il server è sovraccarico. Procedi senza richiesta ad stitch. (Variant)
* Inizia a generare il manifesto di destinazione. (HLSManifestResolver)
* Inizia a generare il manifesto della variante da: URL contenuto. (Variant)
* Inizia a unire gli annunci in manifesto. (VODHLSResolver)
* Tentativo di punto dell&#39;annuncio su `HH:MM:SS`: AdPlacement \[adManifestURL= URL manifesto annuncio, durationSeconds= secondi, ignore= ignore, redirectAd= annuncio di reindirizzamento, priority= priorità.\] \(HLSManifestResolver\)
* Impossibile ottenere gli annunci a causa di una pipeline non valida - ha restituito il contenuto senza annunci. (VOD)
* Impossibile ottenere gli annunci - ha restituito il contenuto senza annunci. (VOD)
* Impossibile ottenere la query dell&#39;annuncio e non è stato fornito alcun URL di contenuto. (VOD)
* URL valido ricevuto. (VOD/Variant)
* Valore Variant M3U8 non trovato. (Variant)

### Record TRACE_PLAYBACK_PROGRESS {#trace-playback-progress-records}

Il server manifest genera record di questo tipo quando riceve un segnale sull&#39;avanzamento della riproduzione durante il flusso di lavoro di tracciamento lato server. I campi oltre `TRACE_PLAYBACK_PROGRESS` vengono visualizzati nell’ordine indicato nella tabella, separati da tabulazioni.

| Campo | Tipo | Descrizione |
|---|---|---|
| status | string | Codice di stato HTTP |
| ampiezza | integer | Larghezza di banda del flusso |
| pts | integer | Tempo PTS nel flusso |
| ms_time | integer | Ora in cui il server manifest ha generato l&#39;URL di tracciamento |
| url | string | URL di reindirizzamento |
| **&quot;** header_user_agent&quot; | string | Intestazione HTTP User-Agent |
| **&quot;** header_dnt&quot; | integer | Intestazione di non tracciamento HTTP |
| **&quot;indirizzo_remoto_** efficace&quot; | string | Indirizzo remoto efficace IPv4 |
| **indirizzo_** remoto | string | Indirizzo remoto IPv4 |

**&quot;** Gli ultimi quattro campi sono facoltativi.

## Flussi a bit rate multiplo {#multiple-bitrate-streams}

Le richieste client per l&#39;inserimento di annunci specificano in genere più di un bit rate nella playlist con formato M3U8 variante. Il server manifest genera e restituisce una nuova variante file M3U8 contenente un collegamento M3U8 separato per ogni bit rate. Genera anche un ID gruppo univoco per collegare questi M3U8s.

Il server manifest utilizza le informazioni nella richiesta dell&#39;URL di Bootstrap del client per recuperare la playlist della variante di contenuto. Genera una nuova playlist variante contenente collegamenti del server manifest al contenuto a livello di flusso. Il client li utilizza per creare richieste di inserimento annunci. I collegamenti di contenuto a livello di flusso del server manifest hanno il seguente formato:

```shell
https://manifest.auditude.com/auditude/{live/vod}/{publisherAssetID}/{rendition}/
{groupID}/{base64-encoded url of the bit rate stream}.[m3u8]?{Query parameters}
```

* **live/**
vodIl server manifest imposta questo valore in base al tipo di playlist del contenuto: Live/lineare (
`#EXT-X-PLAYLIST-TYPE:EVENT`) o VOD (`#EXT-X-PLAYLIST-TYPE:VOD`)

* ****
ID univoco di publisherAssetIDPublisher per il contenuto specifico fornito nella richiesta Bootstrap URL.

* ****
renditionIl server manifest lo imposta in base al 
`BANDWIDTH` del flusso di contenuto e lo utilizza per far corrispondere il bit rate dell&#39;annuncio al bit rate del contenuto. Il bit rate dell’annuncio non può superare il bit rate del contenuto a meno che il rendering dell’annuncio con il bit rate più basso non lo faccia.

* ****
groupIDTil server manifest genera questo valore e lo utilizza per garantire che inserisca gli annunci in modo coerente, indipendentemente dal quale il bit rate esegua il rendering degli annunci da parte del client.

* **url codificato base64 del**
flusso di bit rateIl server manifesto URL-safe base64 codifica l&#39;URL assoluto del flusso di contenuto. Ogni flusso ha il proprio URL.

* **Parametri**
queryParametri query forniti nella richiesta URL Bootstrap.
