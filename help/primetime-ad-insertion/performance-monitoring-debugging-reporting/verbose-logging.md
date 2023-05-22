---
title: Registrazione dettagliata
description: Registrazione dettagliata
copied-description: true
exl-id: f2d1b0c2-ba28-4fba-9a4e-71d1421f37fe
source-git-commit: 3e63c187f12d1bff53370bbcde4d6a77f58f3b4f
workflow-type: tm+mt
source-wordcount: '2155'
ht-degree: 0%

---

# Registrazione dettagliata {#verbose-logging}

## descrizioni degli eventi ptdebug/logging {#ptdebug-logging-events}

Quando si avvia la registrazione di debug per una sessione del server manifesto, è possibile aggiungere `ptdebug` parametro per l&#39;URL della richiesta per specificare le seguenti opzioni per le informazioni restituite dal server manifesto nelle intestazioni HTTP:

* `ptdebug=true`
Tutti i record eccetto TRACE_HTTP_HEADER e la maggior parte dei dati di chiamata/risposta dai record TRACE_AD_CALL.

* `ptdebug=AdCall`
Solo i record di tipo TRACE_AD_ (ad esempio, TRACE_AD_CALL).

* `ptdebug=Header`
Solo record TRACE_HTTP_HEADER.

## Formati dei record di registro {#log-record-formats}

Ogni record di registro ha un tipo e un set di campi, alcuni dei quali potrebbero essere facoltativi. I campi di tutti i record fino al tipo di record sono gli stessi. Forniscono una marca temporale e informazioni sulla sessione. Il tipo di record identifica il tipo di evento registrato e i campi successivi forniscono informazioni sull’evento registrato.

La struttura di un record di registro è la seguente:

`datetime request_id session_id zone_id record_type other fields`.

| Campo | Tipo | Descrizione |
|---|---|---|
| datetime | stringa | Timestamp |
| request_id | stringa | ID richiesta utilizzato dal server manifesto (timestamp Unix) |
| session_id | stringa | ID sessione utilizzato dal server manifesto |
| zone_id | numero intero | Zona |
| record_type | stringa | Tipo di evento da registrare |
| altri campi | varia | Dipende dal tipo di evento |

I record di questo tipo registrano i risultati delle richieste HTTP. Campi oltre `TRACE_REQUEST_INFO` vengono visualizzati nell&#39;ordine indicato nella tabella, separati da tabulazioni.

| Campo | Tipo | Descrizione |
|---|---|---|
| stato | stringa | Codice di stato HTTP restituito |
| request_method | stringa | Metodo HTTP (GET o POST) |
| request_uri | stringa | URI richiesta HTTP (senza host) |
| request_length | numero intero | Lunghezza richiesta (byte) |
| response_length | numero intero | Lunghezza della risposta (byte) |
| delta | numero intero | Tempo (millisecondi) per elaborare la richiesta |
| module_type | stringa | Variante, Flusso o VOD |
| remote_address_aud_client_ip | stringa | **‡** |
| remote_address_x_fwd_for_hdr_key | stringa | **‡** |
| porta_host_remoto | stringa | **‡** |

**‡** Gli ultimi tre campi sono facoltativi.

**Un esempio**

```shell
1427263800524 6495aafc-3f34-4047-ad36-350d4f056eb4 189938TRACE_REQUEST_INFO 301 GET /auditude/variant/pubAsset/aHR0cDov. . ..m3u8?u=cecebae72a919de350b9ac52602623f3&z=189938&ptcueformat=turner& sid =yk-cnnlive-003 &ptdebug=true 0 0 0 Variant 111.22.3.44 111.22.3.45 127.0.0.1:46383
```

### Record TRACE_HTTP_HEADER {#trace-http-header-records}

Record di questo tipo registrano intestazioni HTTP scambiate durante le chiamate HTTP tra il server manifesto e il client, il server di annunci o il server di contenuti. I campi oltre TRACE_HTTP_HEADER vengono visualizzati nell&#39;ordine indicato nella tabella, separati da tabulazioni.

| Campo | Tipo | Descrizione |
|---|---|---|
| request_type | stringa | Tipo di richiesta (PRINCIPALE o SCONOSCIUTO) |
| request_response | stringa | Intestazione di risposta (richiesta o risposta) |
| nome_intestazione | stringa | Nome intestazione HTTP |
| header_value | stringa | Valore intestazione HTTP con codifica Base64 |

>[!NOTE]
>
>Il `request_type` e `header_value` I campi sono facoltativi.

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

I record di questo tipo registrano i risultati delle richieste di annunci del server manifest. Campi oltre `TRACE_AD_CALL` vengono visualizzati nell&#39;ordine indicato nella tabella, separati da tabulazioni.

| Campo | Tipo | Descrizione |
|---|---|---|
| stato | stringa | Codice di stato HTTP restituito |
| request_duration | numero intero | Tempo (millisecondi) dalla richiesta alla risposta |
| ad_server_query_url | stringa | URL per la chiamata dell’annuncio, inclusi i parametri di query |
| ad_system_id | stringa | Sistema di annunci, dalla risposta del server di annunci (Auditude se non specificato) |
| avail_id | stringa | ID del valore, dal cue dell’annuncio nel file del manifesto del contenuto (N/D per VOD) |
| avail_duration | numero | Durata (secondi) del valore disponibile, dalla segnalazione dell’annuncio nel file manifesto del contenuto (N/D per VOD) |
| ad_server_response | stringa | Risposta con codifica Base64 da ad server |

Ecco un esempio:

```shell
2015-03-25T06:13:31.271Z 14272. . . 189938 TRACE_AD_CALL200 8 https://ad.stg2.auditude.com/adserver/a?cip=0.0.0.0&g=1000012&of=1.5 &ptcueformat=turner&ptdebug=true&tl=l,150,30,m&tm=63&u=ceceb. . . Auditude IvpIyC. . . 150 PD94bWw. . .
```

### Record TRACE_AD_INSERT, TRACE_AD_RESOLVE e TRACE_AD_REDIRECT {#trace-ad-insert-resolve-redirect}

I record di questo tipo registrano i risultati delle richieste di annunci indicate dal tipo di record. I campi oltre il tipo di record vengono visualizzati nell&#39;ordine indicato nella tabella, separati da tabulazioni.

| Campo | Tipo | Descrizione |
|---|---|---|
| stato | stringa | Codice di stato HTTP restituito. |
| avail_id | stringa | ID del valore, dal cue dell’annuncio nel file manifesto del contenuto (live) o dal server manifesto (VOD). |
| ad_type | stringa | Tipo di annuncio (DIRECT o REDIRECT). |
| ad_duration | numero intero | Durata (secondi) dell’annuncio, dalla risposta del server di annunci. |
| ad_content_url | stringa | URL del file manifesto dell’annuncio, dalla risposta dell’ad server. |
| **†** ad_content_url_actual | stringa | URL del file manifesto dell’annuncio inserito. Vuoto per TRACE_AD_REDIRECT. |
| ad_system_id | stringa | Sistema di annunci, dalla risposta del server di annunci (Auditude se non specificato). |
| ad_id | stringa | ID dell’annuncio, dalla risposta dell’ad server. |
| creative_id | stringa | ID della creatività, dal nodo dell’annuncio, dalla risposta dell’ad server. |
| **†** ad_call_id | stringa | Non utilizzato. Riservato per uso futuro. |
| delta | numero intero | Tempo (millisecondi) impiegato da questo evento. |
| **†** varie | stringa | L’annuncio del motivo è stato saltato. |

**†** `ad_content_url_actual`, `ad_call_id`, e `misc` I campi sono facoltativi.

>[!NOTE]
>
>Per `TRACE_AD_RESOLVE` e `TRACE_AD_INSERT`, l’URL in `ad_content_url_actual` è per l’annuncio transcodificato, se disponibile. Altrimenti il campo è vuoto per `TRACE_AD_RESOLVE` o uguale a `ad_content_url` per `TRACE_AD_INSERT`.

Ecco un esempio:

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

I record di questo tipo registrano un annuncio creativo mancante. L’unico campo oltre `TRACE_TRANSCODING_NO_MEDIA_TO_TRANSCODE` nella tabella.

| Campo | Tipo | Descrizione |
|---|---|---|
| ad_id | stringa | ID annuncio completo (FQ_AD_ID: Q_AD_ID\[;Q_AD_ID\[;Q_AD_ID...\] \] Q_AD_ID: PROTOCOL:AD_SYSTEM:AD_ID\[:CREATIVE_ID\[:MEDIA_ID\] \] PROTOCOLLO: AUDITUDE,VAST) |

I record di questo tipo registrano i risultati delle richieste di transcodifica inviate dal server di manifesto a CRS. Campi oltre `TRACE_TRANSCODING_REQUESTED` vengono visualizzati nell&#39;ordine indicato nella tabella, separati da tabulazioni.

| Campo | Tipo | Descrizione |
|---|---|---|
| ad_id | stringa | ID annuncio completo |
| ad_manifest_url | stringa | URL del file manifesto dell’annuncio, dalla risposta dell’ad server |
| creative_type | stringa | Tipo di supporto |
| flag | stringa | ID3 indica se la richiesta di transcodifica include una richiesta di aggiunta di un tag ID3 |
| target_duration | stringa | Durata target (secondi) della creatività transcodificata |

I record di questo tipo indicano una richiesta per eseguire il tracciamento lato server. Campi oltre `TRACE_TRACKING_REQUEST` vengono visualizzati nell&#39;ordine indicato nella tabella, separati da tabulazioni.

| Campo | Tipo | Descrizione |
|---|---|---|
| tracking_url_count | numero intero | Numero di URL di tracciamento |
| inizio | galleggiare | Tempo di avvio del frammento PTS (secondi con precisione in millisecondi) |
| fine | galleggiare | Tempo di fine del frammento PTS (secondi con precisione in millisecondi) |

I record di questo tipo forniscono un URL di tracciamento per il tracciamento lato server. Campi oltre `TRACE_TRACKING_REQUEST_URL` vengono visualizzati nell&#39;ordine indicato nella tabella, separati da tabulazioni.

| Campo | Tipo | Descrizione |
|---|---|---|
| timestamp | galleggiare | Tempo (secondi, con precisione .001) all’interno della sessione di riproduzione per eseguire il ping dell’URL di tracciamento. |
| ad_system | stringa | Sistema di annunci (ad esempio, audience) |
| url | stringa | URL per il ping |

Record di questo tipo di richieste di registro effettuate dal server manifesto per `WEBVTT` sottotitoli. Campi oltre `TRACE_WEBVTT_REQUEST` vengono visualizzati nell&#39;ordine indicato nella tabella, separati da tabulazioni.

| Campo | Tipo | Descrizione |
|---|---|---|
| stato | stringa | Codice di stato HTTP restituito |
| vtt_uri | stringa | URL per richiesta |
| inizio | galleggiare | Tempo di inizio suddiviso (secondi con precisione in millisecondi) |
| fine | galleggiare | Tempo di fine divisione (secondi con precisione in millisecondi) |

Record di questo tipo di risposte di registro inviate dal server di manifesto ai client in `answer` alle richieste di `WEBVTT` sottotitoli. Campi oltre `TRACE_WEBVTT_RESPONSE` vengono visualizzati nell&#39;ordine indicato nella tabella, separati da tabulazioni.

| Campo | Tipo | Descrizione |
|---|---|---|
| stato | stringa | Codice di stato HTTP restituito |
| risposta | stringa | Risposta con codifica Base64 inviata al client |

Record di questo tipo rispondono alle richieste effettuate dal server manifesto per `WEBVTT` sottotitoli. Campi oltre `TRACE_WEBVTT_SOURCE` vengono visualizzati nell&#39;ordine indicato nella tabella, separati da tabulazioni.

| Campo | Tipo | Descrizione |
|---|---|---|
| stato | stringa | Codice di stato HTTP restituito |
| sorgente | stringa | Contenuto VTT originale con codifica Base64 |

I record di questo tipo consentono al server manifest di registrare eventi e informazioni non pianificati in altro modo per il momento in cui acquisisce gli annunci. Il campo oltre `TRACE_MISC` è costituito da una stringa di messaggio. I messaggi che potrebbero essere visualizzati includono:

* Annuncio ignorato: AdPlacement \[adManifestURL=https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . . .m3u8, durationSeconds=15.0, ignore=false, redirectAd=false, priority=1\]
* AdPlacement adManifestURL= adManifestURL, durationSeconds= secondi, ignore= ignora, redirectAd= redirectAd, priority= priorità
* Il posizionamento dell’annuncio ha restituito un valore nullo.
* L’annuncio è stato unito.
* Chiamata annuncio non riuscita: messaggio di errore.
* Aggiunta dell’agente utente al recupero del manifesto non elaborato: user-agent.
* Aggiunta di cookie per recuperare il manifesto non elaborato: #
* Messaggio di errore URL richiesto URL non valido. (Impossibile analizzare l’URL della variante)
* Chiamato url: URL ottenuto restituito: codice di risposta. ( URL live)
* Chiamato url: URL return code: response code. ( URL VOD)
* Conflitto rilevato durante la risoluzione degli annunci: una delle due estremità, mid-roll start o mid-roll, rientra nel pre-roll o pre-roll contenuto nel mid-roll (VOD).
* Rilevata eccezione non gestita generata dal gestore per URI: URL richiesta.
* Generazione del manifesto della variante completata. (Variante)
* Generazione del manifesto della variante completata.
* Eccezione nella gestione del reindirizzamento VAST *URL di reindirizzamento *error: error message.
* Impossibile recuperare la playlist dell’annuncio per l’URL del manifesto dell’annuncio.
* Impossibile generare il manifesto di destinazione. (HLSManifestResolver)
* Impossibile analizzare la prima risposta alla chiamata annuncio: messaggio di errore.
* Impossibile elaborare la richiesta *GET|POST *per il percorso: URL della richiesta. (Live/VOD)
* Impossibile elaborare la richiesta del manifesto live: URL della richiesta. (Dal vivo)
* Impossibile restituire un manifesto variante: messaggio di errore.
* Impossibile convalidare l&#39;ID gruppo: ID gruppo.
* Recupero del manifesto non elaborato: URL del contenuto. (Dal vivo)
* Segui reindirizzamento VAST: URL di reindirizzamento.
* Trovate disponibilità vuote. (VOD)
* Trovato *numero* annunci. (VOD)
* Richiesta HTTP ricevuta. (Primo messaggio)
* L’annuncio verrà ignorato perché la differenza tra la durata della risposta dell’annuncio (*durata risposta annuncio *sec) e la durata effettiva dell’annuncio (*durata effettiva *sec) è maggiore del limite. (HLSManifestResolver)
* Il valore che non ha fornito alcun valore ID verrà ignorato. (GroupAdResolver.java)
* Il valore che ha fornito l’ora non valida verrà ignorato: *time *for availId = avail ID.
* Il valore che ha fornito la durata non valida verrà ignorato: *duration *for availId = avail ID.
* Inizializza nuova sessione. (Variante)
* Metodo HTTP non valido. Dev&#39;essere un GET. (VOD)
* Metodo HTTP non valido. La richiesta di tracciamento deve essere un GET. (Dal vivo)
* Messaggio di errore URL richiesto non valido. (Variante)
* Gruppo non valido. (HLSManifestResolver)
* Richiesta non valida. La didascalia non è una richiesta di tracciamento valida. (VOD)
* Richiesta non valida. La richiesta di didascalia deve essere effettuata dopo aver stabilito la sessione. (VOD)
* Richiesta non valida. La richiesta di tracciamento deve essere effettuata dopo aver stabilito la sessione. (VOD)
* Istanza del server non valida per l&#39;ID gruppo di overload: ID gruppo. (Dal vivo)
* È stato raggiunto il limite dei reindirizzamenti VAST - numero.
* Esecuzione di una chiamata dell’annuncio: URL della chiamata dell’annuncio.
* Nessun manifesto trovato per: URL contenuto. (Dal vivo)
* Non è stato trovato alcun risultato corrispondente per l’ID valido: ID valido. (HLSManifestResolver)
* Nessuna sessione di riproduzione trovata. (HLSManifestResolver)
* Elaborazione della richiesta VOD per l’URL del contenuto del manifesto.
* Variante di elaborazione.
* Elaborazione della richiesta di didascalia per l’URL del contenuto del manifesto.
* Elaborazione della richiesta di tracciamento. (VOD)
* Risposta dell’annuncio di reindirizzamento vuota. ( VASTStAX)
* Richiesta: URL.
* Risposta di errore restituita per la richiesta di GET perché non è stata trovata alcuna sessione di riproduzione. (VOD)
* Risposta di errore per la richiesta GET a causa di un errore interno del server.
* Risposta di errore che restituisce la richiesta di GET per specificare una risorsa non valida: ID richiesta annuncio. (VOD)
* Risposta di errore restituita per la richiesta di GET che specifica un ID gruppo non valido o vuoto: ID gruppo. (VOD)
* Risposta di errore restituita per la richiesta di GET che specifica un valore di posizione di tracciamento non valido. (VOD)
* Risposta di errore restituita per la richiesta GET con sintassi non valida: URL richiesta. (Live/VOD)
* Risposta di errore restituita per una richiesta con metodo HTTP non supportato: GET|POST. (Live/VOD)
* Restituzione del manifesto dalla cache. (VOD)
* Il server è sovraccarico. Procedi senza richiesta di unione di annunci. (Variante)
* Inizia a generare il manifesto di destinazione. (HLSManifestResolver)
* Inizia a generare il manifesto della variante da: URL contenuto. (Variante)
* Inizia a unire gli annunci nel manifesto. (VODHLSResolver)
* Tentativo di unire l’annuncio a `HH:MM:SS`: AdPlacement \[adManifestURL= URL manifesto annuncio, durationSeconds= secondi, ignore= ignora, redirectAd= annuncio reindirizzato, priority= priorità.\] \(HLSManifestResolver\)
* Impossibile ottenere gli annunci a causa di una sequenza temporale non valida. È stato restituito il contenuto senza annunci. (VOD)
* Impossibile ottenere gli annunci. È stato restituito il contenuto senza annunci. (VOD)
* Impossibile ottenere la query dell’annuncio e non è stato fornito alcun URL di contenuto. (VOD)
* URL valido ricevuto. (VOD/Variante)
* Variante M3U8 non trovata. (Variante)

### Record TRACE_PLAYBACK_PROGRESS {#trace-playback-progress-records}

Il server manifesto genera record di questo tipo quando riceve un segnale sull&#39;avanzamento della riproduzione durante il flusso di lavoro di tracciamento lato server. Campi oltre `TRACE_PLAYBACK_PROGRESS` vengono visualizzati nell&#39;ordine indicato nella tabella, separati da tabulazioni.

| Campo | Tipo | Descrizione |
|---|---|---|
| stato | stringa | Codice di stato HTTP |
| larghezza di banda | numero intero | Larghezza di banda del flusso |
| pts | numero intero | Tempo PTS all’interno del flusso |
| ms_time | numero intero | Ora in cui il server manifesto ha generato l’URL di tracciamento |
| url | stringa | URL di reindirizzamento |
| **si può** header_user_agent | stringa | Intestazione HTTP dell’agente utente |
| **si può** header_dnt | numero intero | Intestazione Do-Not-Track HTTP |
| **si può** effective_remote_address | stringa | Indirizzo remoto valido IPv4 |
| **si può** indirizzo_remoto | stringa | Indirizzo remoto IPv4 |

**si può** Gli ultimi quattro campi sono facoltativi.

## Più flussi di bit rate {#multiple-bitrate-streams}

Le richieste dei client per l’inserimento di annunci specificano in genere più di una velocità in bit nella variante della playlist in formato M3U8. Il server manifesto genera e restituisce un nuovo file M3U8 variante contenente un collegamento M3U8 separato per ogni velocità bit. Genera anche un ID gruppo univoco per collegare questi M3U8s.

Il server manifest utilizza le informazioni contenute nella richiesta Bootstrap URL del client per recuperare la playlist delle varianti di contenuto. Genera una nuova playlist di varianti contenente i collegamenti del server manifesto al contenuto a livello di flusso. Il client le utilizza per creare richieste di inserimento di annunci. I collegamenti di contenuto a livello di flusso del server manifesto hanno il seguente formato:

```shell
https://manifest.auditude.com/auditude/{live/vod}/{publisherAssetID}/{rendition}/
{groupID}/{base64-encoded url of the bit rate stream}.[m3u8]?{Query parameters}
```

* **live/vod**
Il server manifesto imposta questo valore in base al tipo di playlist del contenuto: Live/linear (
`#EXT-X-PLAYLIST-TYPE:EVENT`) o VOD (`#EXT-X-PLAYLIST-TYPE:VOD`)

* **publisherAssetID**
ID univoco dell’editore per il contenuto specifico fornito nella richiesta URL Bootstrap.

* **rendering**
Il server manifesto imposta questo valore in base al 
`BANDWIDTH` del flusso di contenuto e lo utilizza per far corrispondere la velocità bit dell’annuncio alla velocità bit del contenuto. La velocità in bit dell’annuncio non può superare la velocità in bit del contenuto, a meno che non lo faccia la rappresentazione dell’annuncio con la velocità in bit più bassa.

* **groupID**
Il server manifest genera questo valore e lo utilizza per garantire che inserisca gli annunci in modo coerente, indipendentemente dalla velocità di trasmissione dei rendering richiesta dal client.

* **url con codifica base64 del flusso della velocità in bit**
Il server manifesto URL-safe base64 codifica l&#39;URL assoluto del flusso di contenuto. Ogni flusso ha il proprio URL.

* **Parametri di query**
Parametri di query forniti nella richiesta URL Bootstrap.
