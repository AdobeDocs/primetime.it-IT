---
title: Strumento di debug del server manifesto
description: Strumento di debug del server manifesto
products: SG_PRIMETIME
topic-tags: ad-insertion
discoiqdonotlocalize: false
moreHelpPaths: /content/help/en/primetime/morehelp/ad-insertion;/content/help/en/primetime/morehelp/ad-insertion
pagecreatedat: en
pagelayout: video
sidecolumn: left
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '2414'
ht-degree: 0%

---


# Strumento di debug del server manifesto {#manifest-server-debugging-tool}

Lo strumento di debug consente agli editori di analizzare i problemi di inserimento di annunci potenzialmente costosi esaminando le informazioni di debug restituite in tempo reale dal server manifesto nelle intestazioni HTTP o, quando sono necessarie informazioni più dettagliate, esaminando i registri di sessione dopo il fatto. Partner Adobi come Akamai possono utilizzare lo strumento per eseguire il debug delle loro integrazioni con Primetime ad decisioning.

Lo strumento supporta i problemi di debug e inserimento in una qualsiasi delle configurazioni principali di tracciamento degli annunci del server manifesto:

* Tracciamento lato client con un lettore basato su TVSDK.
* Tracciamento lato client con un lettore non basato su TVSDK.
* Tracciamento lato server.

Per supportare tutti questi casi, lo strumento non richiede o utilizza i codici del publisher del lettore.

Quando avvii una sessione del server manifesto, puoi impostare un parametro sull’URL della richiesta per richiedere di registrare le informazioni di debug. Utilizzando valori diversi di tale parametro, è inoltre possibile richiedere al server manifesto di restituire informazioni di debug specifiche nelle intestazioni HTTP, ma le intestazioni possono contenere solo una quantità limitata di informazioni. È possibile ottenere le credenziali da Adobe per accedere ai file di registro completi, che il server manifesto salva periodicamente (ad esempio ogni ora) su un server di archivio. Una volta ottenute le credenziali per il server, è possibile accedervi direttamente in qualsiasi momento.

<!-- You can also see the [server side event tracking captured in the SSAI dashboard](ssai-debugging-dashboard.md).-->

## Opzioni dello strumento di debug {#debugging-tool-options}

Quando si richiama lo strumento di debug, sono disponibili diverse opzioni per le informazioni restituite dal server manifesto nelle intestazioni HTTP. Le opzioni non influiscono su ciò che il server manifesto inserisce nei file di registro.

### Specifica di ptdebug {#specifying-ptdebug}

Quando si avvia la registrazione di debug per una sessione del server manifesto, è possibile aggiungere il parametro ptdebug all&#39;URL della richiesta per specificare le seguenti opzioni per le informazioni restituite dal server manifesto nelle intestazioni HTTP:

* ptdebug=true Tutti i record tranne `TRACE_HTTP_HEADER` e più `call/response data` da `TRACE_AD_CALL` record.
* ptdebug=Solo AdCall TRACE_AD_*tipo* (ad esempio, TRACE_AD_CALL).
* ptdebug=Header Solo record TRACE_HTTP_HEADER.

Le opzioni non influiscono su ciò che il server manifesto inserisce nei file di registro. Non si ha alcun controllo su questo, ma i file di registro sono file di testo, in modo da poter applicare un&#39;ampia varietà di strumenti per estrarre e riformattare le informazioni che ti interessano.

Ecco un esempio dell’intestazione HTTP restituita quando `ptdebug=Header`. Alcune stringhe lunghe di cifre esadecimali vengono sostituite da `. . .` per chiarezza.

```
X-ADBE-AI-DBG-1 TRACE_MISC    HTTP request received
X-ADBE-AI-DBG-2 TRACE_MISC    Processing Variant
X-ADBE-AI-DBG-3 TRACE_MISC    Valid URL received.
X-ADBE-AI-DBG-4 TRACE_MISC    Initialize new session
X-ADBE-AI-DBG-5 TRACE_MISC    Requesting: /auditude/variant/pubAsset/aHR0cDovL . . .m3u8
 ?u=cecebae . . .&z=189962&pttrackingmode=simple&pttrackingversion=v1
 &ptcueformat=turner&__sid__=yk-sat953pm-112
 &ptdebug=true
X-ADBE-AI-DBG-6  TRACE_HTTP_HEADER  MAIN  REQUEST  Host    bWFuaWZl. . .
X-ADBE-AI-DBG-7  TRACE_HTTP_HEADER  MAIN  REQUEST  Connection       Y2xvc2U=
X-ADBE-AI-DBG-8  TRACE_HTTP_HEADER  MAIN  REQUEST  Accept   dGV4dC. . .
X-ADBE-AI-DBG-9  TRACE_HTTP_HEADER  MAIN  REQUEST  Cookie   c3NhaT. . .
X-ADBE-AI-DBG-10 TRACE_HTTP_HEADER  MAIN  REQUEST  User-Agent       TW96aWxs. . .
X-ADBE-AI-DBG-11 TRACE_HTTP_HEADER  MAIN  REQUEST  Accept-Language  ZW4tdXM=
X-ADBE-AI-DBG-12 TRACE_HTTP_HEADER  MAIN  REQUEST  Accept-Encoding  Z3ppcCwg. . .=
X-ADBE-AI-DBG-13 TRACE_REQUEST_INFO  200   GET
 /auditude/variant/pubAsset/aHR0cD. . ..m3u8
 ?u=cecebae72a919de350b9ac52602623f3&z=189962&pttrackingmode=simple
 &pttrackingversion=v1&ptcueformat=turner&__sid__=yk-sat953pm-112
 &ptdebug=true   0 0 0   Variant  NA  null  null  127.0.0.1:43357
X-ADBE-AI-DBG-14 TRACE_HTTP_HEADER  MAIN  RESPONSE Content-Type     YXBwbG. . .
X-ADBE-AI-DBG-15 TRACE_HTTP_HEADER  MAIN  RESPONSE Cache-Control    bm8tY2. . .
X-ADBE-AI-DBG-16 TRACE_HTTP_HEADER  MAIN  RESPONSE Access-Control-Allow-Origin    Kg==
X-ADBE-AI-DBG-17 TRACE_MISC   Done
```

## Formati dei record di registro {#formats-of-log-records}

Ogni record di registro ha un tipo e un set di campi, alcuni dei quali potrebbero essere facoltativi. I campi di tutti i record fino al tipo di record sono gli stessi. Forniscono una marca temporale e informazioni sulla sessione. Il tipo di record identifica il tipo di evento registrato e i campi successivi forniscono informazioni sull’evento registrato.

La struttura di un record di registro è la seguente:

`datetime request_id session_id zone_id record_type` *altri campi.*

| Campo | Tipo | Descrizione |
|--- |--- |--- |
| datetime | stringa | Timestamp |
| request_id | stringa | ID richiesta utilizzato dal server manifesto (timestamp unix) |
| session_id | stringa | ID sessione utilizzato dal server manifesto |
| zone_id | numero intero | ID zona |
| record_type | stringa | Tipo di evento da registrare |
| altri campi | *** | Dipende dal tipo di evento |

### Record TRACE_REQUEST_INFO {#trace-request-info-records}

I record di questo tipo registrano i risultati delle richieste HTTP. I campi oltre a TRACE_REQUEST_INFO vengono visualizzati nell&#39;ordine indicato nella tabella, separati da tabulazioni.

| Campo | Tipo | Descrizione |
|--- |--- |--- |
| stato | stringa | Codice di stato HTTP restituito |
| request_method | stringa | Metodo HTTP (GET o POST) |
| request_uri | stringa | URI richiesta HTTP (senza host) |
| request_length | numero intero | Lunghezza richiesta (byte) |
| response_length | numero intero | Lunghezza della risposta (byte) |
| delta | numero intero | Tempo (millisecondi) per elaborare la richiesta |
| module_type | stringa | Variante, Flusso o VOD |
| remote_address_aud_client_ip | stringa | (vedere nota) |
| remote_address_x_fwd_for_hdr_key | stringa | (vedere nota) |
| porta_host_remoto | stringa | (vedere nota) |

>[!NOTE]
>
>Gli ultimi tre campi sono facoltativi.

Ecco un esempio:

```
1427263800524 6495aafc-3f34-4047-ad36-350d4f056eb4 189938
TRACE_REQUEST_INFO 301 GET /auditude/variant/pubAsset/aHR0cDov. . ..m3u8
?u=cecebae72a919de350b9ac52602623f3&z=189938&ptcueformat=turner& sid =yk-cnnlive-003 &ptdebug=true 0 0 0 Variant 111.22.3.44 111.22.3.45 127.0.0.1:46383
```

### Record TRACE_HTTP_HEADER {#trace-http-header-records}

Record di questo tipo registrano intestazioni HTTP scambiate durante le chiamate HTTP tra il server manifesto e il client, il server di annunci o il server di contenuti. I campi oltre TRACE_HTTP_HEADER vengono visualizzati nell&#39;ordine indicato nella tabella, separati da tabulazioni.

| Campo | Tipo | Descrizione |
|--- |--- |--- |
| request_type | stringa | Tipo di richiesta (PRINCIPALE o SCONOSCIUTO) |
| request_response | stringa | Intestazione di risposta (richiesta o risposta) |
| nome_intestazione | stringa | Nome intestazione HTTP |
| header_value | stringa | Valore intestazione HTTP con codifica Base64 |

>[!NOTE]
>
>I campi request_type e header_value sono facoltativi.

Ecco un esempio:

```
2015-03-25T06:10:00.927Z  1427263800573  6495aa. . .  189938 TRACE_MISC
    Requesting: /cnn/tvecnn/stream4/stream_Layer.m3u8
2015-03-25T06:10:00.927Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN REQUEST Cookie  aGRu. . .
2015-03-25T06:10:00.928Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN REQUEST User-Agent  TW96aW. . .
2015-03-25T06:10:01.063Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Server  bmd4X2. . .
2015-03-25T06:10:01.063Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Content-Type    YXBwb. . .
2015-03-25T06:10:01.063Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Last-Modified   V2VkL. . .
2015-03-25T06:10:01.063Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  ETag    IjIyY2. . .
2015-03-25T06:10:01.063Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Vary    QWNjZXB. . .
2015-03-25T06:10:01.063Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Cache-Control   bWF4LW. . .
2015-03-25T06:10:01.064Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Expires V2VkL. . .
2015-03-25T06:10:01.064Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Date    V2VkLCA. . .
2015-03-25T06:10:01.064Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Age MQ==
2015-03-25T06:10:01.064Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Via MS4xIH. . .
```

### Record TRACE_AD_CALL {#trace-ad-call-records}

I record di questo tipo registrano i risultati delle richieste di annunci del server manifest. I campi oltre TRACE_AD_CALL vengono visualizzati nell&#39;ordine indicato nella tabella, separati da tabulazioni.

| Campo | Tipo | Descrizione |
|--- |--- |--- |
| stato | stringa | Codice di stato HTTP restituito |
| request_duration | numero intero | Tempo (millisecondi) dalla richiesta alla risposta |
| ad_server_query_url | stringa | URL per la chiamata dell’annuncio, inclusi i parametri di query |
| ad_system_id | stringa | Sistema di annunci, dalla risposta del server di annunci (Auditude se non specificato) |
| avail_id | stringa | ID del valore, dal cue dell’annuncio nel file del manifesto del contenuto (N/D per VOD) |
| avail_duration | numero | Durata (secondi) del valore disponibile, dalla segnalazione dell’annuncio nel file manifesto del contenuto (N/D per VOD) |
| ad_server_response | stringa | Risposta con codifica Base64 da ad server |

Ecco un esempio:

```
2015-03-25T06:13:31.271Z 14272. . . 189938 TRACE_AD_CALL
200 8 https://ad.stg2.auditude.com/adserver/a?cip=0.0.0.0&g=1000012&of=1.5 &ptcueformat=turner&ptdebug=true&tl=l,150,30,m&tm=63&u=ceceb. . . Auditude IvpIyC. . . 150 PD94bWw. . .
```

### Record TRACE_AD_INSERT, TRACE_AD_RESOLVE e TRACE_AD_REDIRECT {#trace-ad-insert-trace-ad-resolve-and-trace-ad-redirect-records}

I record di questo tipo registrano i risultati delle richieste di annunci indicate dal tipo di record. I campi oltre il tipo di record vengono visualizzati nell&#39;ordine indicato nella tabella, separati da tabulazioni.

| Campo | Tipo | Descrizione |
|--- |--- |--- |
| stato | stringa | Codice di stato HTTP restituito |
| avail_id | stringa | ID del valore, dal cue dell’annuncio nel file manifesto del contenuto (live) o dal server manifesto (VOD) |
| ad_type | stringa | Tipo di annuncio (DIRECT o REDIRECT) |
| ad_duration | numero intero | Durata (secondi) dell’annuncio, dalla risposta del server di annunci |
| ad_content_url | stringa | URL del file manifesto dell’annuncio, dalla risposta dell’ad server |
| ad_content_url_actual | stringa | URL del file manifesto dell’annuncio inserito. Vuoto per TRACE_AD_REDIRECT. |
| ad_system_id | stringa | Sistema di annunci, dalla risposta del server di annunci (Auditude se non specificato) |
| ad_id | stringa | ID dell’annuncio, dalla risposta dell’ad server |
| creative_id | stringa | ID della creatività, dal nodo dell’annuncio, dalla risposta dell’ad server |
| ad_call_id | stringa | Non utilizzato. Riservato per uso futuro. |
| delta | numero intero | Tempo (millisecondi) impiegato da questo evento |
| varie | stringa | L’annuncio del motivo è stato saltato |

>[!NOTE]
>
>I campi ad_content_url_actual, ad_call_id e misc sono facoltativi.

Per TRACE_AD_RESOLVE e TRACE_AD_INSERT, l’URL nel campo ad_content_url_actual si riferisce all’annuncio transcodificato, se disponibile. In caso contrario, il campo è vuoto per TRACE_AD_RESOLVE o lo stesso di ad_content_url per TRACE_AD_INSERT.

Ecco un esempio:

```
2015-03-18T22:25:36.229-07:00 1426742736208 1120feb. . . 147465 TRACE_AD_RESOLVE
200 0 DIRECT 15 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8 Auditude 308008 0  cecebae72a919de350b9ac52602623f3 0 NA

2015-03-18T22:25:36.230-07:00 1426742736208 1120feb. . . 147465 TRACE_AD_RESOLVE
200 2 DIRECT 15 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8 Auditude 308008 0  cecebae72a919de350b9ac52602623f3 0 NA

2015-03-18T22:25:36.562-07:00 1426742736208 1120feb. . . 147465 TRACE_AD_INSERT
200 0 DIRECT 15 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8
Auditude 308008 0 cecebae72a919de350b9ac52602623f3 0 NA
2015-03-18T22:25:36.563-07:00 1426742736208 1120feb. . . 147465 TRACE_AD_INSERT
200 2 DIRECT 15 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8
Auditude 308008 0 cecebae72a919de350b9ac52602623f3 0 NA
```

### Record TRACE_TRACKING_URL {#trace-tracking-url-records}

I record di questo tipo registrano i risultati delle richieste di annunci del server manifest. I campi oltre TRACE_TRACKING_URL vengono visualizzati nell&#39;ordine indicato nella tabella, separati da tabulazioni.

| Campo | Tipo | Descrizione |
|--- |--- |--- |
| pts | numero | Timestamp del programma. Tempo all’interno del video per chiamare l’URL. |
| ad_system | stringa | Sistema di annunci (controllo o ruota libera) |
| url | stringa | URL con ping |
| stato | stringa | Stato HTTP restituito dal ping |

Ecco un esempio:

```
2015-06-04T23:24:42.000-0700    1426742736208     3086f5cd . . .    12345    TRACE_TRACKING_URL
    0.000000    ExampleSystem    https://localhost/index.php?stream:test#8.1433485415;
    sid:3086f5cd . . .;pts:0    200
```

### Record TRACE_TRANSCODING_NO_MEDIA_TO_TRANSCODE {#trace-transcoding-no-media-to-transcode-records}

I record di questo tipo registrano un annuncio creativo mancante. Nella tabella viene visualizzato l&#39;unico campo oltre a TRACE_TRANSCODING_NO_MEDIA_TO_TRANSCODE.

| Campo | Tipo | Descrizione |
|--- |--- |--- |
| ad_id | stringa | ID annuncio completo `(FQ_AD_ID: Q_AD_ID\[;Q_AD_ID\[;Q_AD_ID...\]\]` Q_AD_ID: `PROTOCOL:AD_SYSTEM:AD_ID\[:CREATIVE_ID\[:MEDIA_ID\]\]` PROTOCOLLO: AUDITUDE, VAST) |

### Record TRACE_TRANSCODING_REQUESTED {#trace-transcoding-requested-records}

I record di questo tipo registrano i risultati delle richieste di transcodifica inviate dal server di manifesto a CRS. I campi oltre a TRACE_TRANSCODING_REQUESTED vengono visualizzati nell&#39;ordine indicato nella tabella, separati da tabulazioni.

| Campo | Tipo | Descrizione |
|--- |--- |--- |
| ad_id | stringa | ID annuncio completo |
| ad_manifest_url | stringa | URL del file manifesto dell’annuncio, dalla risposta dell’ad server |
| creative_type | stringa | Tipo di supporto |
| flag | stringa | ID3 indica se la richiesta di transcodifica include una richiesta di aggiunta di un tag ID3 |
| target_duration | stringa | Durata target (secondi) della creatività transcodificata |

### Record TRACE_TRACKING_REQUEST {#trace-tracking-request-records}

I record di questo tipo indicano una richiesta per eseguire il tracciamento lato server. I campi oltre TRACE_TRACKING_REQUEST vengono visualizzati nell&#39;ordine indicato nella tabella, separati da tabulazioni.

| Campo | Tipo | Descrizione |
|--- |--- |--- |
| tracking_url_count | numero intero | Numero di URL di tracciamento |
| inizio | galleggiare | Tempo di avvio del frammento PTS (secondi con precisione in millisecondi) |
| fine | galleggiare | Tempo di fine del frammento PTS (secondi con precisione in millisecondi) |

### Record TRACE_TRACKING_REQUEST_URL {#trace-tracking-request-url-records}

I record di questo tipo forniscono un URL di tracciamento per il tracciamento lato server. I campi oltre a TRACE_TRACKING_REQUEST_URL vengono visualizzati nell&#39;ordine indicato nella tabella, separati da tabulazioni.

| Campo | Tipo | Descrizione |
|--- |--- |--- |
| timestamp | galleggiare | Tempo (secondi, con precisione .001) all’interno della sessione di riproduzione per eseguire il ping dell’URL di tracciamento |
| ad_system | stringa | Sistema di annunci (ad esempio, audience) |
| url | stringa | URL per il ping |

### Record TRACE_WEBVTT_REQUEST {#trace-webvtt-request-records}

Record di questo tipo di registro richieste effettuate dal server di manifesto per le didascalie WEBVTT. I campi oltre TRACE_WEBVTT_REQUEST vengono visualizzati nell&#39;ordine indicato nella tabella, separati da tabulazioni.

| Campo | Tipo | Descrizione |
|--- |--- |--- |
| stato | stringa | Codice di stato HTTP restituito |
| vtt_uri | stringa | URL per richiesta |
| inizio | galleggiare | Tempo di inizio suddiviso (secondi con precisione in millisecondi) |
| fine | galleggiare | Tempo di fine divisione (secondi con precisione in millisecondi) |

### Record TRACE_WEBVTT_RESPONSE {#trace-webvtt-response-records}

Record ``of ``questo ``type ``log ``responses ``il ``manifest ``server ``sends ``a ``clients ``in `` `answer` ``a ``requests `` `for` ``WEBVTT ``sottotitoli. I campi oltre TRACE_WEBVTT_RESPONSE &quot;vengono visualizzati nell&#39;ordine indicato nella tabella, separati `by`schede.

| Campo | Tipo | Descrizione |
|--- |--- |--- |
| stato | stringa | Codice di stato HTTP restituito |
| risposta | stringa | Risposta con codifica Base64 inviata al client |

### Record TRACE_WEBVTT_SOURCE {#trace-webvtt-source-records}

Record di questo tipo rispondono alle richieste effettuate dal server manifesto per le didascalie WEBVTT. I campi oltre TRACE_WEBVTT_SOURCE vengono visualizzati nell&#39;ordine indicato nella tabella, separati da tabulazioni.

| Campo | Tipo | Descrizione |
|--- |--- |--- |
| stato | stringa | Codice di stato HTTP restituito |
| sorgente | stringa | Contenuto VTT originale con codifica Base64 |


### Record TRACE_MISC {#trace-misc-records}

I record di questo tipo consentono al server manifest di registrare eventi e informazioni non pianificati in altro modo per il momento in cui acquisisce gli annunci. Il campo oltre TRACE_MISC è costituito da una stringa di messaggio. I messaggi che potrebbero essere visualizzati includono:

* Annuncio ignorato :AdPlacement `[adManifestURL=https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . . .m3u8, durationSeconds=15.0, ignore=false, redirectAd=false, priority=1]`
* AdPlacement adManifestURL=*adManifestURL*, durationSeconds=*secondi*, ignora=*ignora*, redirectAd=*redirectAd*, priorità=*priorità*
* Il posizionamento dell’annuncio ha restituito un valore nullo.
* L’annuncio è stato unito.
* Chiamata annuncio non riuscita: *messaggio di errore*.
* Aggiunta dell’agente utente per recuperare il manifesto non elaborato: *user-agent*.
* Aggiunta di cookie per recuperare il manifesto non elaborato: [cookie]
* URL non valido *messaggio di errore URL richiesto*. (Impossibile analizzare l’URL della variante)
* URL chiamato: URL *ha restituito: codice di risposta*. ( URL live)
* URL chiamato: URL *codice restituito: codice di risposta*. ( URL VOD)
* Conflitto rilevato durante la risoluzione degli annunci: una delle due estremità, mid-roll start o mid-roll, rientra nel pre-roll o pre-roll contenuto nel mid-roll (VOD).
* Rilevata eccezione non gestita generata dal gestore per l&#39;URI: *URL richiesta*.
* Generazione del manifesto della variante completata. (Variante)
* Generazione del manifesto della variante completata.
* Eccezione nella gestione di reindirizzamento VAST *URL di reindirizzamento *error: *messaggio di errore*.
* Impossibile recuperare la playlist dell&#39;annuncio per *URL del manifesto dell’annuncio*.
* Impossibile generare il manifesto di destinazione. (HLSManifestResolver)
* Impossibile analizzare la prima risposta della chiamata annuncio: *messaggio di errore*.
* Impossibile elaborare la richiesta *GET|POST *per il percorso: *URL richiesta*. (Live/VOD)
* Impossibile elaborare la richiesta del manifesto live: *URL richiesta*. (Dal vivo)
* Impossibile restituire un manifesto variante: *messaggio di errore*.
* Impossibile convalidare l&#39;ID gruppo: *ID gruppo*.
* Recupero del manifesto non elaborato: *URL contenuto*. (Dal vivo)
* Segui reindirizzamento VAST: *URL di reindirizzamento*.
* Trovate disponibilità vuote. (VOD)
* Trovato *numero *annunci. (VOD)
* Richiesta HTTP ricevuta. (Primo messaggio)
* L’annuncio verrà ignorato perché la differenza tra la durata della risposta dell’annuncio (*durata risposta annuncio *sec) e la durata effettiva dell’annuncio (*durata effettiva *sec) è maggiore del limite. (HLSManifestResolver)
* Il valore che non ha fornito alcun valore ID verrà ignorato. (GroupAdResolver.java)
* Il valore di ora fornito non valido verrà ignorato: *time *for availId = *ID disponibile*.
* Il valore di durata fornito non valido verrà ignorato: *duration *for availId = *ID disponibile*.
* Inizializza nuova sessione. (Variante)
* Metodo HTTP non valido. Dev&#39;essere un GET. (VOD)
* Metodo HTTP non valido. La richiesta di tracciamento deve essere un GET. (Dal vivo)
* URL non valido *messaggio di errore URL richiesto*. (Variante)
* Gruppo non valido. (HLSManifestResolver)
* Richiesta non valida. La didascalia non è una richiesta di tracciamento valida. (VOD)
* Richiesta non valida. La richiesta di didascalia deve essere effettuata dopo aver stabilito la sessione. (VOD)
* Richiesta non valida. La richiesta di tracciamento deve essere effettuata dopo aver stabilito la sessione. (VOD)
* Istanza del server non valida per l&#39;ID del gruppo di overload: *ID gruppo*. (Dal vivo)
* Limite di reindirizzamenti VAST raggiunto - *numero*.
* Effettuare una chiamata annuncio: *URL della chiamata dell’annuncio*.
* Nessun manifesto trovato per: *URL contenuto*. (Dal vivo)
* Nessun risultato corrispondente trovato per l&#39;ID valido: *ID disponibile*. (HLSManifestResolver)
* Nessuna sessione di riproduzione trovata. (HLSManifestResolver)
* Elaborazione della richiesta VOD per il manifesto *URL contenuto*.
* Variante di elaborazione.
* Elaborazione richiesta didascalia per manifesto *URL contenuto*.
* Elaborazione della richiesta di tracciamento. (VOD)
* Risposta dell’annuncio di reindirizzamento vuota. ( VASTStAX)
* Richiesta: *URL*.
* Risposta di errore restituita per la richiesta di GET perché non è stata trovata alcuna sessione di riproduzione. (VOD)
* Risposta di errore per la richiesta GET a causa di un errore interno del server.
* Risposta di errore restituita per una richiesta di GET che specifica una risorsa non valida: *ID richiesta annuncio*. (VOD)
* Risposta di errore restituita per la richiesta di GET che specifica un ID gruppo non valido o vuoto: *ID gruppo*. (VOD)
* Risposta di errore restituita per la richiesta di GET che specifica un valore di posizione di tracciamento non valido. (VOD)
* Risposta di errore restituita per la richiesta GET con sintassi non valida - *URL richiesta*. (Live/VOD)
* Risposta di errore restituita per la richiesta con metodo HTTP non supportato: *GET|POST*. (Live/VOD)
* Restituzione del manifesto dalla cache. (VOD)
* Il server è sovraccarico. Procedi senza richiesta di unione di annunci. (Variante)
* Inizia a generare il manifesto di destinazione. (HLSManifestResolver)
* Inizia a generare il manifesto della variante da: *URL contenuto*. (Variante)
* Inizia a unire gli annunci nel manifesto. (VODHLSResolver)
* Tentativo di unire l’annuncio a `HH:MM:SS`: AdPlacement \[adManifestURL=*URL manifesto annuncio*, durationSeconds=*secondi*, ignora=*ignora*, redirectAd=*redirect ad*, priorità=*priorità*.\]
* Impossibile ottenere gli annunci a causa di una sequenza temporale non valida. È stato restituito il contenuto senza annunci. (VOD)
* Impossibile ottenere gli annunci. È stato restituito il contenuto senza annunci. (VOD)
* Impossibile ottenere la query dell’annuncio e non è stato fornito alcun URL di contenuto. (VOD)
* URL valido ricevuto. (VOD/Variante)
* Variante M3U8 non trovata. (Variante)

### Record TRACE_TRACKING_URL {#trace-tracking-url-records-1}

Il server manifest genera record di questo tipo dopo aver chiamato un URL di tracciamento durante il flusso di lavoro di tracciamento lato server. I campi oltre TRACE_TRACKING_URL vengono visualizzati nell&#39;ordine indicato nella tabella, separati da tabulazioni.

| Campo | Tipo | Descrizione |
|--- |--- |--- |
| pts | numero | Tempo PTS all’interno del flusso |
| ad_system | stringa | Sistema pubblicitario dell’annuncio (audience o ruota libera) |
| url | stringa | URL con ping |
| stato | stringa | Codice di stato HTTP |

### Record TRACE_PLAYBACK_PROGRESS {#trace-playback-progress-records}

Il server manifesto genera record di questo tipo quando riceve un segnale sull&#39;avanzamento della riproduzione durante il flusso di lavoro di tracciamento lato server. I campi oltre TRACE_PLAYBACK_PROGRESS vengono visualizzati nell&#39;ordine indicato nella tabella, separati da tabulazioni.

| Campo | Tipo | Descrizione |
|--- |--- |--- |
| stato | stringa | Codice di stato HTTP |
| larghezza di banda | numero intero | Larghezza di banda del flusso |
| pts | numero intero | Tempo PTS all’interno del flusso |
| ms_time | numero intero | Ora in cui il server manifesto ha generato l’URL di tracciamento |
| url | stringa | URL di reindirizzamento |
| header_user_agent | stringa | Intestazione HTTP dell’agente utente |
| header_dnt | numero intero | Intestazione Do-Not-Track HTTP |
| effective_remote_address | stringa | Indirizzo remoto valido IPv4 |
| indirizzo_remoto | stringa | Indirizzo remoto IPv4 |

>[!NOTE]
>
>Gli ultimi quattro campi sono facoltativi.

## Risorse utili {#helpful-resources}

* Consulta la documentazione completa dell’Aiuto all’indirizzo [Informazioni e supporto per Adobe Primetime](https://helpx.adobe.com/support/primetime.html) pagina.
