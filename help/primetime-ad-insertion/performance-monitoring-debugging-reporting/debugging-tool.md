---
title: Strumento di debug server manifesto
seo-title: Strumento di debug server manifesto
description: Strumento di debug server manifesto
seo-description: Strumento di debug server manifesto
uuid: 0b4f06f5-4b1f-4f88-980a-5b4df28e0094
products: SG_PRIMETIME
topic-tags: ad-insertion
discoiquuid: 00b49659-ce56-4b5c-87cd-c357a0936641
donotlocalize: false
moreHelpPaths: /content/help/en/primetime/morehelp/ad-insertion;/content/help/en/primetime/morehelp/ad-insertion
pagecreatedat: en
pagelayout: video
sidecolumn: left
translation-type: tm+mt
source-git-commit: d5e948992d7c59e80b530c8f4619adbffc3c03d8
workflow-type: tm+mt
source-wordcount: '2422'
ht-degree: 0%

---


# Strumento di debug server manifesto {#manifest-server-debugging-tool}

Lo strumento di debug consente agli editori di esaminare i problemi di inserimento di annunci potenzialmente costosi esaminando le informazioni di debug restituite in tempo reale dal server del manifesto nelle intestazioni HTTP o, quando sono necessarie informazioni più dettagliate, esaminando i registri di sessione dopo il fatto.  partner di Adobe come Akamai possono utilizzare lo strumento per eseguire il debug delle integrazioni con le decisioni relative agli annunci Primetime.

Lo strumento supporta il debug e l&#39;inserimento di problemi in una qualsiasi delle configurazioni principali del server manifesto e del tracciamento:

* Tracciamento lato client con un lettore basato su TVSDK.
* Tracciamento lato client con un lettore non basato su TVSDK.
* Tracciamento lato server.

Per supportare tutti questi casi, lo strumento non richiede o utilizza codici editore del lettore.

Quando avviate una sessione del server di manifesto, potete impostare un parametro sull&#39;URL della richiesta in modo da chiedere di registrare le informazioni di debug. Utilizzando valori diversi di tale parametro, potete anche chiedere al server di manifesto di restituire determinate informazioni di debug nelle intestazioni HTTP, ma le intestazioni possono contenere solo una quantità limitata di informazioni. È possibile ottenere le credenziali da  Adobe per accedere ai file di registro completi, che il server manifesto salva periodicamente (ad esempio ogni ora) in un server di archivio. Una volta ottenute le credenziali per quel server, potete accedervi direttamente in qualsiasi momento.

<!-- You can also see the [server side event tracking captured in the SSAI dashboard](ssai-debugging-dashboard.md).-->

## Opzioni dello strumento di debug {#debugging-tool-options}

Quando si richiama lo strumento di debug, sono disponibili diverse opzioni per le informazioni restituite dal server manifesto nelle intestazioni HTTP. Le opzioni non influiscono sulle posizioni del server manifesto nei file di registro.

### Specifica di ptdebug {#specifying-ptdebug}

Quando avviate la registrazione di debug per una sessione del server manifesto, potete aggiungere il parametro ptdebug all&#39;URL della richiesta per specificare le seguenti opzioni per le informazioni restituite dal server manifesto nelle intestazioni HTTP:

* ptdebug=true Tutti i record tranne `TRACE_HTTP_HEADER` e la maggior parte `call/response data` dai record `TRACE_AD_CALL`.
* ptdebug=AdCall Only TRACE_AD_*type* (ad esempio, TRACE_AD_CALL).
* ptdebug=Solo intestazione record TRACE_HTTP_HEADER.

Le opzioni non influiscono sulle posizioni del server manifesto nei file di registro. Non si ha alcun controllo su questo, ma i file di registro sono file di testo, in modo da poter applicare un&#39;ampia varietà di strumenti per estrarre e riformattare le informazioni che vi interessano.

Di seguito è riportato un esempio dell&#39;intestazione HTTP restituita quando `ptdebug=Header`. Alcune stringhe lunghe di cifre esadecimali sono sostituite da `. . .` per maggiore chiarezza.

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

Ogni record di registro ha un tipo e un set di campi, alcuni dei quali potrebbero essere facoltativi. I campi di tutti i record fino al tipo di record sono gli stessi. Forniscono una marca temporale e informazioni sulla sessione. Il tipo di record identifica il tipo di evento da registrare e i campi successivi forniscono informazioni sull&#39;evento registrato.

La struttura di un record di registro è la seguente:

`datetime request_id session_id zone_id record_type` *altri campi.*

| Field | Tipo | Descrizione |
|--- |--- |--- |
| datetime | string | Timestamp |
| request_id | string | ID richiesta utilizzato dal server manifesto (timestamp univoci) |
| session_id | string | ID sessione utilizzato dal server manifesto |
| zone_id | integer | ID zona |
| record_type | string | Tipo di evento da registrare |
| altri campi | *** | Dipende dal tipo di evento |

### TRACE_REQUEST_INFO record {#trace-request-info-records}

I record di questo tipo registrano i risultati delle richieste HTTP. I campi oltre TRACE_REQUEST_INFO vengono visualizzati nell&#39;ordine indicato nella tabella, separati da tabulazioni.

| Field | Tipo | Descrizione |
|--- |--- |--- |
| status | string | Codice di stato HTTP restituito |
| request_method | string | Metodo HTTP (GET o POST) |
| request_uri | string | URI richiesta HTTP (senza host) |
| request_length | integer | Lunghezza della richiesta (byte) |
| response_length | integer | Lunghezza della risposta (byte) |
| delta | integer | Tempo (millisecondi) per elaborare la richiesta |
| module_type | string | Variante, Flusso o VOD |
| remote_address_aud_client_ip | string | (vedi nota) |
| remote_address_x_fwd_for_hdr_key | string | (vedi nota) |
| remote_host_port | string | (vedi nota) |

>[!NOTE]
>
>Gli ultimi tre campi sono facoltativi.

Esempio:

```
1427263800524 6495aafc-3f34-4047-ad36-350d4f056eb4 189938
TRACE_REQUEST_INFO 301 GET /auditude/variant/pubAsset/aHR0cDov. . ..m3u8
?u=cecebae72a919de350b9ac52602623f3&z=189938&ptcueformat=turner& sid =yk-cnnlive-003 &ptdebug=true 0 0 0 Variant 111.22.3.44 111.22.3.45 127.0.0.1:46383
```

### Record TRACE_HTTP_HEADER {#trace-http-header-records}

Record di questo tipo di intestazioni HTTP del registro scambiate durante le chiamate HTTP tra il server manifesto e il client, il server di annunci o il server del contenuto. I campi oltre TRACE_HTTP_HEADER vengono visualizzati nell’ordine indicato nella tabella, separati da tabulazioni.

| Field | Tipo | Descrizione |
|--- |--- |--- |
| request_type | string | Tipo di richiesta (PRINCIPALE o SCONOSCIUTA) |
| request_response | string | Intestazione risposta (richiesta o risposta) |
| header_name | string | Nome intestazione HTTP |
| header_value | string | Valore dell&#39;intestazione HTTP con codifica Base64 |

>[!NOTE]
>
>I campi request_type e header_value sono facoltativi.

Esempio:

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

### TRACE_AD_CALL record {#trace-ad-call-records}

I record di questo tipo registrano i risultati delle richieste di annunci server manifest. I campi oltre a TRACE_AD_CALL vengono visualizzati nell’ordine indicato nella tabella, separati da tabulazioni.

| Field | Tipo | Descrizione |
|--- |--- |--- |
| status | string | Codice di stato HTTP restituito |
| request_Duration | integer | Tempo (millisecondi) dalla richiesta alla risposta |
| ad_server_query_url | string | URL per la chiamata di annuncio, inclusi i parametri di query |
| ad_system_id | string | Ad system, dalla risposta del server di annunci (Auditude se non specificato) |
| avail_id | string | ID del valore, dal cue point dell&#39;annuncio nel file manifesto del contenuto (N/D per VOD) |
| avail_Duration | number | Durata (secondi) del valore, dal cue point dell&#39;annuncio nel file manifesto del contenuto (N/D per VOD) |
| ad_server_response | string | Risposta con codifica Base64 dal server di annunci |

Esempio:

```
2015-03-25T06:13:31.271Z 14272. . . 189938 TRACE_AD_CALL
200 8 https://ad.stg2.auditude.com/adserver/a?cip=0.0.0.0&g=1000012&of=1.5 &ptcueformat=turner&ptdebug=true&tl=l,150,30,m&tm=63&u=ceceb. . . Auditude IvpIyC. . . 150 PD94bWw. . .
```

### record TRACE_AD_INSERT, TRACE_AD_RESOLVE e TRACE_AD_REDIRECT {#trace-ad-insert-trace-ad-resolve-and-trace-ad-redirect-records}

I record di questo tipo registrano i risultati delle richieste di annunci indicate dal tipo di record. I campi oltre il tipo di record vengono visualizzati nell&#39;ordine indicato nella tabella, separati da tabulazioni.

| Field | Tipo | Descrizione |
|--- |--- |--- |
| status | string | Codice di stato HTTP restituito |
| avail_id | string | ID del valore, dal cue point dell&#39;annuncio nel file manifesto del contenuto (live) o dal server manifesto (VOD) |
| ad_type | string | Tipo di annuncio (DIRECT o REDIRECT) |
| ad_Duration | integer | Durata (secondi) dell&#39;annuncio, dalla risposta del server dell&#39;annuncio |
| ad_content_url | string | URL del file manifesto dell&#39;annuncio, dalla risposta del server dell&#39;annuncio |
| ad_content_url_effective | string | URL del file manifesto dell&#39;annuncio inserito. Vuoto per TRACE_AD_REDIRECT. |
| ad_system_id | string | Ad system, dalla risposta del server di annunci (Auditude se non specificato) |
| ad_id | string | ID dell&#39;annuncio, dalla risposta del server di annunci |
| creative_id | string | ID del creativo, dal nodo dell&#39;annuncio, dalla risposta del server dell&#39;annuncio |
| ad_call_id | string | Non utilizzato. Riservato per uso futuro. |
| delta | integer | Tempo (millisecondi) impiegato da questo evento |
| misc | string | Motivo annuncio ignorato |

>[!NOTE]
>
>I campi ad_content_url_effective, ad_call_id e misc sono facoltativi.

Per TRACE_AD_RESOLVE e TRACE_AD_INSERT, l’URL nel campo ad_content_url_effective è relativo all’annuncio transcodificato, se disponibile. In caso contrario, il campo è vuoto per TRACE_AD_RESOLVE o come ad_content_url per TRACE_AD_INSERT.

Esempio:

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

### TRACE_TRACKING_URL record {#trace-tracking-url-records}

I record di questo tipo registrano i risultati delle richieste di annunci server manifest. I campi oltre a TRACE_TRACKING_URL vengono visualizzati nell&#39;ordine indicato nella tabella, separati da tabulazioni.

| Field | Tipo | Descrizione |
|--- |--- |--- |
| pts | number | Timestamp del programma. Tempo all’interno del video per richiamare l’URL. |
| ad_system | string | Sistema pubblicitario (auditudine o ruota libera) |
| url | string | URL con cerniera |
| status | string | Stato HTTP restituito dal ping |

Esempio:

```
2015-06-04T23:24:42.000-0700    1426742736208     3086f5cd . . .    12345    TRACE_TRACKING_URL
    0.000000    ExampleSystem    https://localhost/index.php?stream:test#8.1433485415;
    sid:3086f5cd . . .;pts:0    200
```

### TRACE_TRANSCODING_NO_MEDIA_TO_TRANSCODE record {#trace-transcoding-no-media-to-transcode-records}

I record di questo tipo registrano un annuncio creativo mancante. Nella tabella viene visualizzato l’unico campo oltre TRACE_TRANSCODING_NO_MEDIA_TO_TRANSCODE.

| Field | Tipo | Descrizione |
|--- |--- |--- |
| ad_id | string | ID annuncio completo `(FQ_AD_ID: Q_AD_ID\[;Q_AD_ID\[;Q_AD_ID...\]\]` Q_AD_ID: PROTOCOLLO `PROTOCOL:AD_SYSTEM:AD_ID\[:CREATIVE_ID\[:MEDIA_ID\]\]`: AUDITUDE,VAST) |

### TRACE_TRANSCODING_REQUESTED record {#trace-transcoding-requested-records}

I record di questo tipo registrano i risultati delle richieste di transcodifica inviate dal server manifesto a CRS. I campi oltre TRACE_TRANSCODING_REQUESTED vengono visualizzati nell&#39;ordine indicato nella tabella, separati da tabulazioni.

| Field | Tipo | Descrizione |
|--- |--- |--- |
| ad_id | string | ID annuncio completo |
| ad_manifest_url | string | URL del file manifesto dell&#39;annuncio, dalla risposta del server dell&#39;annuncio |
| creative_type | string | Tipo di supporto |
| flag | string | ID3 indica se la richiesta di transcodifica include una richiesta per aggiungere un tag ID3 |
| target_Duration | string | Durata target (secondi) del creativo transcodificato |

### TRACE_TRACKING_REQUEST record {#trace-tracking-request-records}

I record di questo tipo indicano una richiesta di tracciamento lato server. I campi oltre TRACE_TRACKING_REQUEST vengono visualizzati nell&#39;ordine indicato nella tabella, separati da tabulazioni.

| Field | Tipo | Descrizione |
|--- |--- |--- |
| tracking_url_count | integer | Numero di URL di tracciamento |
| start | float | Tempo di inizio del frammento PTS (secondi con precisione in millisecondi) |
| end | float | Tempo di fine del frammento PTS (secondi con precisione in millisecondi) |

### TRACE_TRACKING_REQUEST_URL record {#trace-tracking-request-url-records}

I record di questo tipo forniscono un URL di tracciamento per il tracciamento lato server. I campi oltre TRACE_TRACKING_REQUEST_URL vengono visualizzati nell’ordine indicato nella tabella, separati da tabulazioni.

| Field | Tipo | Descrizione |
|--- |--- |--- |
| timestamp | float | Tempo (secondi, con precisione 0,001) nella sessione di riproduzione per il ping dell’URL di tracciamento |
| ad_system | string | Ad system (ad esempio, auditude) |
| url | string | URL del ping |

### TRACE_WEBVTT_REQUEST record {#trace-webvtt-request-records}

Record di questo tipo di richieste di registro eseguite dal server manifesto per le didascalie WEBVTT. I campi oltre TRACE_WEBVTT_REQUEST vengono visualizzati nell&#39;ordine indicato nella tabella, separati da tabulazioni.

| Field | Tipo | Descrizione |
|--- |--- |--- |
| status | string | Codice di stato HTTP restituito |
| vtt_uri | string | URL per richiesta |
| start | float | Ora inizio divisione (secondi con precisione in millisecondi) |
| end | float | Tempo di fine diviso (secondi con precisione in millisecondi) |

### TRACE_WEBVTT_RESPONSE record {#trace-webvtt-response-records}

Registra ``of ``questo ``type ``log ``responses ``il ``manifest ``server ``sends ``su ``clients ``in `` `answer` ``a ``requests `` `for` ``WEBVTT ``didascalie. I campi oltre TRACE_WEBVTT_RESPONSE &quot;vengono visualizzati nell&#39;ordine indicato nella tabella, con le `by`schede separate.

| Field | Tipo | Descrizione |
|--- |--- |--- |
| status | string | Codice di stato HTTP restituito |
| response | string | Risposta con codifica Base64 inviata al client |

### TRACE_WEBVTT_SOURCE record {#trace-webvtt-source-records}

Record di questo tipo di risposte del registro alle richieste fatte dal server manifesto per le didascalie WEBVTT. I campi oltre a TRACE_WEBVTT_SOURCE vengono visualizzati nell&#39;ordine indicato nella tabella, separati da tabulazioni.

| Field | Tipo | Descrizione |
|--- |--- |--- |
| status | string | Codice di stato HTTP restituito |
| source | string | Contenuto VTT originale con codifica Base64 |


### TRACE_MISC record {#trace-misc-records}

I record di questo tipo consentono al server di manifesto di registrare eventi e informazioni non altrimenti pianificate per l&#39;acquisizione di annunci. Il campo oltre TRACE_MISC è costituito da una stringa di messaggio. I messaggi che potrebbero essere visualizzati includono:

* Annuncio ignorato:AdPlacement `[adManifestURL=https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . . .m3u8, durationSeconds=15.0, ignore=false, redirectAd=false, priority=1]`
* AdPlacement adManifestURL=*adManifestURL*, durataSeconds=*secondi*, ignore=*ignore*, redirectAd=*redirectAd*, priorità=*priority*
* La posizione dell&#39;annuncio ha restituito null.
* Annuncio bloccato.
* Chiamata annuncio non riuscita: *messaggio di errore*.
* Aggiunta di agente utente per recuperare il manifesto non elaborato: *user-agent*.
* Aggiunta di cookie per recuperare il manifesto non elaborato: [cookie]
* URL non valido *messaggio di errore URL richiesto*. (Impossibile analizzare l&#39;URL della variante)
* URL denominato: URL *restituito: codice di risposta*. (Live URL)
* URL denominato: URL *codice restituito: codice di risposta*. (URL VOD)
* È stato rilevato un conflitto durante la risoluzione degli annunci: uno dei due elementi: inizio medio o fine medio-rollio rientra nel pre-rollio o prerotolo contenuto nel mid-roll (VOD).
* Rilevata eccezione non gestita generata dal gestore per URI: *richiedere l&#39;URL*.
* Generazione del manifesto della variante completata. (Variante)
* Generazione del manifesto della variante completata.
* Eccezione nella gestione del reindirizzamento VAST *URL di reindirizzamento *errore: *messaggio di errore*.
* Impossibile recuperare la playlist dell&#39;annuncio per *URL manifesto annuncio*.
* Impossibile generare il manifesto di destinazione. (HLSManifestResolver)
* Impossibile analizzare la risposta della prima chiamata ad: *messaggio di errore*.
* Impossibile elaborare *GET|POST *richiesta percorso: *richiedere l&#39;URL*. (Live/VOD)
* Impossibile elaborare la richiesta del manifesto live: *richiedere l&#39;URL*. (Live)
* Impossibile restituire un manifesto di variante: *messaggio di errore*.
* Impossibile convalidare l&#39;ID gruppo: *ID gruppo*.
* Recupero del manifesto non elaborato: *URL contenuto*. (Live)
* Dopo il reindirizzamento VAST: *reindirizzare l&#39;URL*.
* Trovate delle risorse vuote. (VOD)
* Trovato *numero *annunci. (VOD)
* Richiesta HTTP ricevuta. (Primo messaggio)
* L&#39;annuncio viene ignorato perché la differenza tra la durata della risposta dell&#39;annuncio (*durata della risposta *sec) e la durata effettiva dell&#39;annuncio (*durata effettiva *sec) è maggiore del limite. (HLSManifestResolver)
* Ignorare un valore che non ha fornito alcun valore ID. (GroupAdResolver.java)
* Valore che ha fornito un valore di ora non valido ignorato: *tempo *per availId = *ID valido*.
* Il valore che ha fornito un valore di durata non valido viene ignorato: *durata *per availId = *ID valido*.
* Inizializza nuova sessione. (Variante)
* Metodo HTTP non valido. Deve essere un GET. (VOD)
* Metodo HTTP non valido. La richiesta di tracciamento deve essere un GET. (Live)
* URL non valido *messaggio di errore URL richiesto*. (Variante)
* Gruppo non valido. (HLSManifestResolver)
* Richiesta non valida. Didascalia non è una richiesta di tracciamento valida. (VOD)
* Richiesta non valida. La richiesta di didascalia deve essere eseguita dopo che è stata stabilita la sessione. (VOD)
* Richiesta non valida. La richiesta di tracciamento deve essere eseguita dopo che è stata stabilita la sessione. (VOD)
* Istanza del server non valida per l&#39;ID del gruppo di sovraccarico: *ID gruppo*. (Live)
* Limite di reindirizzamenti VAST raggiunti - *number*.
* Chiamata ad annunci: *ad call URL*.
* Nessun manifesto trovato per: *URL contenuto*. (Live)
* Nessun valore corrispondente trovato per l&#39;ID valido: *ID valido*. (HLSManifestResolver)
* Nessuna sessione di riproduzione trovata. (HLSManifestResolver)
* Elaborazione della richiesta VOD per manifesto *URL contenuto*.
* Variante di elaborazione.
* Elaborazione della richiesta di didascalia per l&#39;URL di contenuto manifesto **.
* Elaborazione della richiesta di tracciamento. (VOD)
* Reindirizza risposta annuncio vuota. (VASTStAX)
* Richiesta: *URL*.
* Risposta di errore di ritorno per la richiesta di GET perché non è stata trovata alcuna sessione di riproduzione. (VOD)
* Risposta di errore restituita per la richiesta di GET a causa di un errore interno del server.
* Risposta di errore di ritorno per la richiesta di GET che specifica una risorsa non valida: *ID richiesta annuncio*. (VOD)
* Risposta di errore di ritorno per la richiesta di GET che specifica un ID gruppo vuoto o non valido: *ID gruppo*. (VOD)
* Risposta di errore restituita per la richiesta di GET che specifica un valore di posizione di tracciamento non valido. (VOD)
* Risposta di errore restituita per la richiesta di GET con sintassi non valida - *richiesta URL*. (Live/VOD)
* Risposta di errore di ritorno per la richiesta con metodo HTTP non supportato: *GET|POST*. (Live/VOD)
* Restituzione del manifesto dalla cache. (VOD)
* Il server è sovraccarico. Procedete senza richiesta di punto e punto. (Variante)
* Iniziate a generare il manifesto di destinazione. (HLSManifestResolver)
* Avvia la generazione del manifesto della variante da: *URL contenuto*. (Variante)
* Iniziate a raggruppare gli annunci in manifest. (VODHLSResolver)
* Tentativo di cucire l&#39;annuncio su `HH:MM:SS`: AdPlacement \[adManifestURL=*ad Manifest URL*, durataSeconds=*secondi*, ignore=*ignore*, redirectAd=*redirect ad*, priorità=*priority*.]
* Impossibile ottenere gli annunci a causa di una cronologia pitimeline non valida - ha restituito il contenuto senza annunci. (VOD)
* Impossibile ottenere gli annunci: è stato restituito il contenuto senza annunci. (VOD)
* Impossibile ottenere la richiesta di annuncio e non è stato fornito alcun URL di contenuto. (VOD)
* URL ricevuto valido. (VOD/Variant)
* Impossibile trovare la variante M3U8. (Variante)

### TRACE_TRACKING_URL record {#trace-tracking-url-records-1}

Il server manifesto genera record di questo tipo dopo aver chiamato un URL di tracciamento durante il flusso di lavoro di tracciamento lato server. I campi oltre a TRACE_TRACKING_URL vengono visualizzati nell&#39;ordine indicato nella tabella, separati da tabulazioni.

| Field | Tipo | Descrizione |
|--- |--- |--- |
| pts | number | Tempo PTS nel flusso |
| ad_system | string | Ad&#39;s ad system (auditudine o ruota libera) |
| url | string | URL con cerniera |
| state | string | Codice di stato HTTP |

### TRACE_PLAYBACK_PROGRESS record {#trace-playback-progress-records}

Il server manifesto genera record di questo tipo quando riceve un segnale sull’avanzamento della riproduzione durante il flusso di lavoro di tracciamento lato server. I campi oltre a TRACE_PLAYBACK_PROGRESS vengono visualizzati nell&#39;ordine indicato nella tabella, separati da tabulazioni.

| Field | Tipo | Descrizione |
|--- |--- |--- |
| status | string | Codice di stato HTTP |
| larghezza | integer | Larghezza di banda del flusso |
| pts | integer | Tempo PTS nel flusso |
| ms_time | integer | Ora in cui il server manifesto ha generato l’URL di tracciamento |
| url | string | URL di reindirizzamento |
| header_user_agent | string | Intestazione agente utente HTTP |
| header_dnt | integer | Intestazione non traccia HTTP |
| effective_remote_address | string | Indirizzo remoto IPv4 efficace |
| remote_address | string | Indirizzo remoto IPv4 |

>[!NOTE]
>
>Gli ultimi quattro campi sono facoltativi.

## Risorse utili {#helpful-resources}

* Consulta la documentazione completa della guida in linea alla pagina [ Informazioni e supporto per Adobe Primetime](https://helpx.adobe.com/support/primetime.html).
