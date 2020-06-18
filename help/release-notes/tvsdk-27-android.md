---
title: TVSDK 2.7 per Android - Note sulla versione
seo-title: TVSDK 2.7 per Android - Note sulla versione
description: Note sulla versione di TVSDK 2.7 per Android descrivono le novità o le modifiche, i problemi risolti e noti e i problemi del dispositivo in TVSDK Android 2.7
seo-description: Note sulla versione di TVSDK 2.7 per Android descrivono le novità o le modifiche, i problemi risolti e noti e i problemi del dispositivo in TVSDK Android 2.7
uuid: 4013b97d-29f9-435b-8772-b19df7054282
products: SG_PRIMETIME
topic-tags: release-notes
discoiquuid: bab78e9f-f9ba-4e1c-b778-0936ae704037
translation-type: tm+mt
source-git-commit: 9c6a6f0b5ecff78796e37daf9d7bdb9fa686ee0c
workflow-type: tm+mt
source-wordcount: '4123'
ht-degree: 0%

---


# TVSDK 2.7 per Android - Note sulla versione {#tvsdk-for-android-release-notes}

Note sulla versione di TVSDK 2.7 per Android descrivono le novità o le modifiche, i problemi risolti e noti e i problemi del dispositivo in TVSDK Android 2.7

## TVSDK Android 2.7 {#tvsdk-android}

Il lettore di riferimento Android è incluso con Android TVSDK nella directory samples/ della distribuzione. Il file README&lt;.md di accompagnamento spiega come creare il lettore di riferimento.

>[!NOTE]
>
>Per generare correttamente il lettore di riferimento, come descritto in README.md distribuito con la release, accertatevi di effettuare le seguenti operazioni:
>
>1. Scaricate VideoHeartbeat.jar da [https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases](https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases) (libreria VideoHeartbeat per Android v2.0.0)
>1. Estrai VideoHeartbeat.jar nella cartella libs/.
>



## Nuove funzioni {#new-features}

TVSDK 2.7 per Android include tutte le funzioni della versione 1.4 eccetto le funzioni non supportate elencate in Matrice [di](#feature-matrix)funzioni.

**Android TVSDK 2.7**

* **Supporto per la risoluzione di annunci paralleli**

TVSDK 2.7 supporta la risoluzione simultanea di tutte le richieste di annunci in un&#39;interruzione pubblicitaria, invece della risoluzione sequenziale.

### Nuove funzioni nelle versioni precedenti {#new-features-previous-releases}

**Versione 2.5.6**

* **TVSDK 2.5 supporta Android P**
* **Abilitazione dell&#39;audio sullo sfondo**

   Per abilitare la riproduzione audio quando l’app passa dal primo piano allo sfondo, l’app deve invocare l’API enableAudioPlaybackInBackground di MediaPlayer con true come argomento quando il lettore è nello stato PREPARATO.

* **alwaysUseAudioOutputLatency(valore booleano) nella classe MediaPlayer**

Se impostata, utilizzate la latenza di output nel calcolo della marca temporale audio.
Valore dei parametri booleani - True utilizzerà la latenza di output audio nel calcolo delle marche temporali audio.

* **Ottimizzato per ottenere la migliore esperienza di riproduzione anche se la velocità della larghezza di banda scende improvvisamente.**
TVSDK ora annulla il download in corso del segmento, se necessario, e passa in modo dinamico alla rappresentazione appropriata. Questo avviene passando senza soluzione di continuità tra i bitrate senza interruzioni.

**Versione 2.5.5**

* **Inserimento con interruzioni pubblicitarie parziali**

   Esperienza simile a quella televisiva di partecipare nel mezzo di un annuncio pubblicitario senza attivare il tracciamento per l&#39;annuncio parzialmente guardato.\
   Esempio**: **L&#39;utente si unisce al centro (a 40 secondi) di un annuncio pubblicitario di 90 secondi composto da tre annunci da 30 secondi. Questo è 10 secondi dopo il secondo annuncio nell&#39;interruzione.
   * Il secondo annuncio viene riprodotto per la durata rimanente (20 sec) seguita dal terzo annuncio.
   * I tracciatori annunci per l’annuncio parziale riprodotto (secondo annuncio) non vengono attivati. I tracciatori solo per il terzo annuncio vengono attivati.

* **Proteggere il caricamento di annunci tramite HTTPS**

   Adobe Primetime fornisce un&#39;opzione per richiedere la prima chiamata a server di annunci primetime e CRS attraverso https.

* **Aggiunto AdSystem e Creative Id alle richieste CRS**

   * Ora includendo &#39;AdSystem&#39; e &#39;CreativeId&#39; come nuovi parametri nelle richieste 1401 e 1403.

* **L&#39;API setEncodeUrlForTracking nella classe NetworkConfiguration rimossa** come caratteri non sicuri in un URL deve essere codificata.

**Versione 2.5.4**

Android TVSDK v2.5.4 offre i seguenti aggiornamenti e modifiche API:

* Le modifiche nel valore predefinito per il valore WebViewDebbugingWebViewDebbuging sono impostate su False per impostazione predefinita. Per attivarlo, chiama setWebContentsDebuggingEnabled(true) nell&#39;applicazione.
* Aggiornamento della versione OpenSSL e CurlAggiornamento della libreria alla versione v7.57.0 e di OpenSSL alla versione 1.0.2k.
* Accesso a livello di app per l&#39;oggetto di risposta VASTintrodotto un nuovo API NetworkAdInfo::getVastXml() che fornisce l&#39;accesso dell&#39;oggetto di risposta VAST all&#39;applicazione.

**Versione 2.5.3**

Android TVSDK v2.5.3 offre i seguenti aggiornamenti e modifiche API.

* Tutti i clienti TVSDK che utilizzano CRS sono invitati ad aggiornare le proprie app con TVSDK 2.5.3.85 o versioni successive su Android. Questo sarà un componente aggiuntivo per l&#39;implementazione dell&#39;app esistente. Dopo l&#39;aggiornamento di TVSDK, verifica la presenza di richieste URL creative CRS in uno strumento proxy (ad esempio: Charles) e confermate che il nome e la versione dell&#39;host nel percorso riflettano come nella struttura URL di esempio seguente.

   `https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784 bf3586d.m3u8`

* Agente utente TVSDK personalizzabile: sono state aggiunte nuove API per personalizzare gli agenti utente.

   * setCustomUserAgent(valore String)
   * getCustomUserAgent()

* Condividi cookie tra l’applicazione Android e TVSDK: Android TVSDK ora supporta l&#39;accesso ai cookie tra il livello JAVA (memorizzato in CookieStore dell&#39;applicazione Android) e il livello TVSDK C++. Ora, è possibile impostare e/o modificare i cookie in livello C++ nativo in quanto saranno esposti a Java Cookie Store.
* Modifiche API:

   * Viene aggiunto un nuovo evento CookiesUpdatedEvent. Viene inviato dal lettore multimediale quando il cookie viene aggiornato.
   * Viene aggiunta una nuova API a NetworkConfiguration::set/ getCustomUserAgent() per utilizzare l&#39;agente utente personalizzato.
   * A NetworkConfiguration viene aggiunta una nuova API::set/ getEncodedUrlForTracking per imporre la codifica dei caratteri non sicuri.
   * A NetworkConfiguration viene aggiunta una nuova API::getNetworkDownVerificationUrl() per impostare un URL di verifica della rete in caso di failover.
   * Viene aggiunta una nuova proprietà a TextFormat::dealSpaceAsAlphaNum che definisce se lo spazio deve essere trattato come alfanumerico durante la visualizzazione delle didascalie.

* Modifiche in SizeAvailableEvent: Precedentemente, i metodi getHeight() e getWidth() di SizeAvailableEvent in 2.5.2 venivano utilizzati per restituire l&#39;altezza e la larghezza del fotogramma, che venivano restituiti dal formato multimediale. Ora restituisce l&#39;altezza e la larghezza di output rispettivamente restituiti dal decodificatore.
* Modifiche nel comportamento Buffering: Il comportamento di buffering viene modificato. È lasciata allo sviluppatore di app su quello che desiderano fare in caso di buffer vuoto. 2.5.3 utilizza la dimensione del buffer di riproduzione in una situazione vuota del buffer.

**Versione 2.5.2**

Android TVSDK v2.5.2 offre importanti correzioni di bug e alcune modifiche API.

**Versione 2.5.1**

Le nuove importanti funzionalità rilasciate in Android 2.5.1.

* **Miglioramenti** delle prestazioniLa nuova architettura TVSDK 2.5.1 apporta una serie di miglioramenti delle prestazioni. Sulla base delle statistiche di uno studio di benchmarking di terze parti, la nuova architettura offre una riduzione di 5 volte del tempo di avvio e 3,8 volte inferiore rispetto alla media del settore:

   * **Instant on per VOD e live -** Quando si attiva l&#39;istante, TVSDK inizializza e bufferizza i contenuti multimediali prima dell&#39;avvio della riproduzione. Poiché potete avviare più istanze di MediaPlayerItemLoader contemporaneamente in background, potete creare un buffer per più flussi. Quando un utente cambia il canale e il flusso si trova correttamente nel buffer, la riproduzione sul nuovo canale inizia immediatamente. TVSDK 2.5.1 supporta anche l&#39;opzione Instant On per flussi **live** . I flussi live vengono inseriti nuovamente nel buffer quando la finestra live si sposta.

      * **Logica ABR migliorata -** La nuova logica ABR si basa sulla lunghezza del buffer, sulla velocità di modifica della lunghezza del buffer e sulla larghezza di banda misurata. In questo modo, l&#39;ABR sceglie il bit rate corretto quando la larghezza di banda oscilla e ottimizza anche il numero di volte in cui l&#39;interruttore del bitrate avviene effettivamente monitorando la velocità con cui cambia la lunghezza del buffer.
      * **Download parziale del segmento/Sottosegmentazione: TVSDK riduce ulteriormente le dimensioni di ciascun frammento, per avviare la riproduzione il prima possibile.** Il frammento ts deve avere un fotogramma chiave ogni due secondi.
      * **Lazy ad resolution -** TVSDK non attende la risoluzione degli annunci non preroll prima di avviare la riproduzione, riducendo così il tempo di avvio. Le API come ricerca e trucco non sono ancora consentite fino alla risoluzione di tutti gli annunci. Questo è applicabile ai flussi VOD utilizzati con CSAI. Operazioni come ricerca e avanzamento rapido non sono consentite fino al completamento della risoluzione dell&#39;annuncio. Per i flussi live questa funzione non può essere abilitata per la risoluzione degli annunci durante un evento live.
      * **Connessioni di rete persistenti: questa funzione consente a TVSDK di creare e memorizzare un elenco interno di connessioni di rete persistenti.** Tali connessioni vengono riutilizzate per più richieste, anziché aprire una nuova connessione per ogni richiesta di rete e quindi distruggerla successivamente. Questo aumenta l&#39;efficienza e diminuisce la latenza nel codice di rete, consentendo prestazioni di riproduzione più veloci.
Quando TVSDK apre una connessione, richiede al server una connessione *keep-alive* . Alcuni server potrebbero non supportare questo tipo di connessione, nel qual caso TVSDK tornerà a stabilire una connessione per ogni richiesta. Inoltre, mentre per impostazione predefinita le connessioni persistenti sono attivate, TVSDK dispone ora di un&#39;opzione di configurazione che consente alle app di disattivare le connessioni persistenti, se necessario.
      * **Download parallelo: il download di video e audio in parallelo anziché in serie riduce i ritardi di avvio.** Questa funzione consente la riproduzione di file HLS Live e VOD, ottimizza l&#39;utilizzo della larghezza di banda disponibile da un server, riduce la probabilità di trovarsi in situazioni di sovraccarico del buffer e riduce al minimo il ritardo tra il download e la riproduzione.
      * **Download di annunci in parallelo -** TVSDK prerileva gli annunci in parallelo alla riproduzione del contenuto prima di colpire le interruzioni pubblicitarie, consentendo così la riproduzione senza soluzione di continuità di annunci e contenuti.

* **Riproduzione**

   * **Riproduzione dei contenuti MP4 -** le clip brevi MP4 non devono essere transcodificate per essere riprodotte in TVSDK.
Nota: Per la riproduzione MP4 non sono supportati lo switching ABR, la riproduzione a trucco, l&#39;inserimento di annunci, la rilegatura audio tardiva e la segmentazione secondaria.
   * **Riproduzione dei mattoni con bitrate adattivo (ABR) -** Questa funzione consente a TVSDK di passare da un flusso all&#39;altro in modalità di riproduzione a trucco. Potete utilizzare profili non iFrame per eseguire la riproduzione a velocità più basse.
   * **Riproduzione con trucco più fluido -** Questi miglioramenti migliorano l&#39;esperienza dell&#39;utente:

          * Bitrate adattivo e frame rate selezionati durante la riproduzione, in base alla larghezza di banda e al profilo
          buffer* Utilizzo del flusso principale invece del flusso IDR per ottenere una riproduzione rapida fino a 30 fps.
      
* **Protezione dei contenuti**

   * **Protezione dell&#39;uscita basata sulla risoluzione - Questa funzione associa le restrizioni di riproduzione a risoluzioni specifiche, fornendo controlli DRM più precisi.**

* **Supporto dei flussi di lavoro**

   * **Direct Billing Integration -** invia le metriche di fatturazione al back-end Adobe  Analytics, certificato da Adobe Primetime per i flussi utilizzati dal cliente.
TVSDK raccoglie automaticamente le metriche, rispettando il contratto di vendita del cliente per generare rapporti di utilizzo periodici richiesti a scopo di fatturazione. A ogni evento di inizio flusso, TVSDK utilizza l&#39;API di inserimento dati Adobe  Analytics per inviare metriche di fatturazione come il tipo di contenuto, i flag abilitati per l&#39;inserimento di annunci e i flag abilitati per l&#39;abilitazione di drm, in base alla durata del flusso fatturabile, alla suite di rapporti di proprietà di Adobe  Analytics Primetime. Ciò non interferisce con le suite di rapporti Adobe  Analytics o le chiamate server del cliente, né viene incluso in esse. Su richiesta, questo rapporto sull&#39;utilizzo della fatturazione viene inviato periodicamente ai clienti. Questa è la prima fase della funzione di fatturazione che supporta solo la fatturazione dell&#39;utilizzo. Può essere configurato in base al contratto di vendita utilizzando le API descritte nella documentazione. Questa funzione è abilitata per impostazione predefinita. Per disattivare questa funzione, fare riferimento al campione del lettore di riferimento.
   * **Supporto per il failover migliorato: sono state implementate** strategie aggiuntive per continuare la riproduzione senza interruzioni, nonostante gli errori dei server host, dei file playlist e dei segmenti.

* **Pubblicità**

   * **Integrazione con Moat** - Supporto per la misurazione della visibilità degli annunci da Moat.
   * **Banner pubblicitari-** I banner Companion vengono visualizzati insieme a un annuncio lineare e spesso continuano a essere visualizzati sulla vista al termine dell&#39;annuncio. Questi banner possono essere di tipo html (uno snippet HTML) o di tipo iframe (un URL per una pagina iframe).

* **Analytics**

   * **VHL 2.0 -** Si tratta dell&#39;ultima integrazione ottimizzata per Video Heartbeats Library (VHL) per la raccolta automatica dei dati di utilizzo per Adobe  Analytics. La complessità delle API è stata ridotta per semplificare l&#39;implementazione. Scaricate la libreria VHL [v2.0.0 per Android](https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases) ed estraete il file JAR nella cartella libs.

* **SizeAvaliableEventListener**
   * i metodi getHeight() e getWidth() di SizeAvailableEvent restituiranno ora l&#39;output rispettivamente in altezza e larghezza. Le proporzioni di visualizzazione possono essere calcolate come segue:

      ```
      SizeAvailableEvent e;
      
      DAR = e.getWidth()/ e.getHeight();
      
      Storage Aspect Ratio in terms of Sar width and Sar height can also be used to calculate Frame width and Frame height:
      
      SAR = e.getSarWidth()/e.getSarHeight();
      
      frameHeight = e.getHeight();
      
      frameWidth = e.getWidth()/SAR;    
      ```

* **Cookie**

   * Android TVSDK ora supporta l&#39;accesso ai cookie JAVA memorizzati in CookieStore dell&#39;applicazione Android. Viene fornita un’API di callback (onCookiesUpdated) per la registrazione ogni volta che un nuovo cookie viene fornito come parte dell’intestazione di risposta &quot;Set-Cookie&quot;. Questi cookie sono disponibili come elenco di cookie HttpCookie utilizzati per un URI/dominio diverso impostando questi valori di cookie su tale URI/dominio utilizzando CookieStore. Analogamente, i valori dei cookie in TVSDK vengono aggiornati utilizzando l&#39;API di aggiunta CookieStore.

## Matrice di funzioni {#feature-matrix}

TVSDK per Android supporta una serie di funzioni che potete implementare per aggiungere funzionalità alle applicazioni video.

Nelle tabelle delle funzioni riportate di seguito, un &#39;Y&#39; indica che la funzione è supportata nella versione corrente.

| Feature | Tipo di contenuto | HLS |
|---|---|---|
| Riproduzione generale (Riproduci, Pausa, Cerca) | VOD + Live | Y |
| FER - Riproduzione generale (riproduzione, pausa, ricerca) | FER VOD | Y |
| Cercare quando viene riprodotto un annuncio | VOD + Live | Non supportato |
| AC3 | VOD + Live | Non supportato |
| MP3 | VOD | Non supportato |
| Riproduzione di contenuti MP4 | VOD | Y |
| Logica di commutazione bitrate adattivo | VOD + Live | Y |
| Riproduzione solo audio | VOD + Live | Y |
| Supporto per più CDN | VOD + Live | Non supportato |
| Riproduzione di annunci con supporti solo audio | VOD + Live | Non supportato |
| Sottotitoli codificati - 608/708 | VOD + Live | Y |
| Sottotitoli codificati - WebVTT | VOD + Live | Y |
| Failover manifesto | VOD + Live | Y |
| Failover avanzato | VOD + Live | Y |
| Notifiche QoS e del lettore | VOD + Live | Y |
| Supporto per le intestazioni dei cookie | VOD + Live | Y |
| Supporto per intestazioni HTTP personalizzate | VOD + Live | Y (consentire l&#39;inserimento nell&#39;elenco obbligatorio) |
| Impostare i parametri di controllo del buffer | VOD + Live | Y |
| Impostare controlli bitrate adattivi | VOD + Live | Y |
| Tag Manifest Personalizzati | VOD + Live | Y |
| Rilegatura audio tardiva | VOD + Live | Y |
| 302 Redirect | VOD + Live | Y |
| Riproduzione con offset | VOD + Live | Y |
| Riproduzione solo audio | VOD + Live | Y |
| Gioco di mattoni | VOD + Live | Y |
| Lento movimento in riproduzione su mattoni | VOD + Live | Non supportato |
| Gioca a mattoni liscia (con ABR) | VOD + Live | Y |
| Analisi ID3 | VOD + Live | Y |
| Blackout degli annunci | VOD + Live | Non supportato |
| Instant On | VOD + Live | Non supportato |
| Supporto dei marcatori di discontinuità | VOD + Live | Y |
| 302 Distinzione di reindirizzamento | VOD + Live | Y |

| Feature | Tipo di contenuto | HLS |
|---|---|---|
| Riproduzione generale, annunci attivati | VOD + Live | Y |
| Contenuto FER con annunci abilitati | VOD | Y |
| Comportamenti annuncio predefiniti | VOD + Live | Y |
| VAST 2.0/3.0 | VOD + Live | Y |
| VMAP 1.0 | VOD + Live | Y |
| Annunci MP4 | VOD + Live | Y (da CRS) |
| Gioco di mattoni con annunci attivati | VOD + Live | Y |
| Solo annunci | VOD | Y |
| Parametri di targeting | VOD + Live | Y |
| Parametri personalizzati | VOD + Live | Y |
| Comportamenti annuncio personalizzati | VOD + Live | Y |
| Tag Ad Personalizzati | Live | Y |
| Risolutori annunci personalizzati | VOD + Live | Y |
| Risolutore annunci personalizzato a ruota libera | VOD | Y |
| C3 | VOD + Live | Non supportato |
| Lazy Ad Resolve | VOD | Y |
| Supporto dei marcatori di discontinuità - SSAI | VOD + Live | Y |
| Annunci per la compagnia, Annunci per banner e Annunci cliccabili | VOD + Live | Y |
| VPAID 2.0 | VOD + Live | Y (JS) |
| Uscita Annuncio Precoce | Live | Y |
| Definizione delle priorità creative basate su regole | VOD + Live | Y |
| Regole CRS | VOD + Live | Y |
| JSON Ad Resolver | VOD + Live | Non supportato |
| Integrazione Moat | VOD + Live | Y |

| Feature | Tipo di contenuto | HLS |
|---|---|---|
| Crittografia AES | VOD + Live | Y |
| Cifratura AES di esempio | VOD + Live | Y |
| Flussi token | VOD + Live | Y |
| DRM | VOD + Live | Solo DRM Primetime (futuro) Widevine) |
| Riproduzione esterna (RBOP) | VOD + Live | Solo Primetime DRM |
| Rotazione licenza | VOD + Live | Solo Primetime DRM |
| Rotazione chiave | VOD + Live | Solo Primetime DRM |

| Feature | Tipo di contenuto | HLS |
|---|---|---|
| Integrazione Adobe  Analytics VHL | VOD + Live | Y |
| Fatturazione | VOD + Live | Y |

## Problemi risolti {#resolved-issues}

Se la risoluzione è associata a un problema segnalato, viene visualizzato un riferimento Zendesk, ad esempio ZD#xxxxx

**Android TVSDK 2.7**

Questa sezione fornisce un riepilogo del problema risolto nella release di TVSDK 2.7.

* ZD#37166 - La chiamata di tracciamento degli errori viene attivata anche quando l&#39;annuncio viene riprodotto correttamente.
* ZD#37134 - Gli Ad ID errati vengono restituiti, nel caso, wrapper(3P) Ad è presente con più annunci nella risposta VMAP.

**Android TVSDK 2.5.6**

* ZD #34992 - La lingua è vuota nei sottotitoli codificati.
   * È stato corretto un caso in cui TVSDK non stava analizzando #EXT-X-MEDIA:TYPE=CLOSED-CAPTIONS dal manifesto principale per ottenere i dettagli della traccia della didascalia.
* ZD #35078 - Convalida P Android.
   * TVSDK 2.5.6 è stato convalidato con le ultime build Android P beta. Nessun problema riscontrato a causa del nuovo sistema operativo Android.
* ZD #34149 - Il lettore continua a richiedere manifesti anche se si verifica un errore.
   * È stato corretto il caso in cui TVSDK effettuava chiamate ripetitive anche quando tutti i profili erano disattivati (errore 404).
* ZD #31533 - Riproduzione dell&#39;audio su Android dopo che l&#39;app è stata inviata in background.
   * È stata aggiunta l&#39; `enableAudioPlaybackInBackground` API di MediaPlayer che dovrebbe essere chiamata con &#39;True&#39; come argomento (quando il lettore è in stato PREPARATO) per abilitare la riproduzione dell&#39;audio quando l&#39;app è in background.

**Android TVSDK 2.5.5**

* ZD #21647 - Android TVSDK notifica 640x368 quando la dimensione effettiva del video è 640x360.
   * A causa della variabile m_nOutputHeight (all&#39;interno di AndroidMCVideoDecoder) che viene aggiornata con l&#39;altezza del fotogramma invece dell&#39;altezza effettiva dell&#39;output. Sono state apportate modifiche rilevanti alla funzione getVideoFrame per calcolare correttamente m_nOutputHeight.
* ZD #26614 - Urgente — 3rd party ad serving / programmatic — mancata trasmissione delle impressioni.
   * Migliorata la correzione precedente gestendo il caso in analisi XML dove il problema era riproducibile quando &quot;space&quot; è prima del segno &quot;uguale&quot; come &lt;VAST version =&quot;2.0&quot;>
* ZD #29296 - Android: Aggiungete AdSystem e Creative ID alle richieste CRS.
   * Ora includendo &#39;AdSystem&#39; e &#39;CreativeId&#39; come nuovi parametri nelle richieste 1401 e 1403.
* ZD #33062 - TVSDK si arresta in modo anomalo all&#39;occorrenza del carattere di pipe nella risposta VAST sotto il nodo CDATA
   * API setEncodeUrlForTracking nella classe NetworkConfiguration rimossa come caratteri non sicuri in un URL da codificare.
* ZD #33063 - Logica di selezione file CRS interrotta. TVSDK non inviava la richiesta CRS per il formato Web ma la inviava invece per i file 3gpp.
   * È stata corretta la logica ora. Quando si utilizzano file multimediali con webm e formato 3gpp, CRS richiede di essere inviato per il webm. E utilizzando entrambi i file multimediali con formato 3gpp, la richiesta CRS da inviare per il file 3gpp con bitrate più alto.
* ZD #33125 - Arresti anomali dell&#39;app Android con specifico tag DoubleClick all&#39;interno del VMAP.
   * È stato corretto lo scenario per evitare l’arresto anomalo.
* ZD #32256 - Problema di rotazione della licenza e rotazione della chiave - Adobe Access.
   * È stata corretta l&#39;inizializzazione dei segmenti con i metadati DRM per il contenuto SampleAES. Funziona perfettamente con i contenuti AES128.
* ZD #33619 - Avanzamento rapido di un contenuto playlist in crescita bloccato nello stato di buffering vicino al punto dal vivo.
   * È stato gestito il caso durante l&#39;attraversamento del punto dal vivo in modalità di riproduzione trucco.
* ZD #34151 - Oggetti TimedMetadata non ordinati.
   * Se appartenevano alla stessa ora nella timeline, venivano visualizzati in ordine casuale due eventi TimedMetadata. Mantenimento dell&#39;ordine originale in manifesto.
* ZD #34189 - Problema quando si cerca di iniziare l&#39;interruzione dell&#39;annuncio.
   * Il problema era con gli annunci SSAI che sono cuciti con discontinuità. E la causa era un comportamento quando cerchiamo di iniziare tali annunci, cerchiamo un fotogramma chiave e non lo troviamo. Il motivo era che la marca temporale audio minima dell&#39;annuncio era precedente alla marca temporale del video principale. Quindi, finiamo per cercare un fotogramma chiave in presenza di dati frammentDump errati. È stato corretto.
* ZD #34528 - La risoluzione video non viene aggiornata oltre 640x360 su un dongle FireTV di terza generazione.
   * Migliorata la correzione per includere gli aggiornamenti firmware più recenti.
* ZD #34793 - TVSDK 2.5.x utilizzato per arrestarsi in modo anomalo con il risolutore di contenuti personalizzato in alcuni casi in cui VideoEngine presupponeva che le impostazioni di auditudeSettings fossero disponibili e non lo fossero.
   * L&#39;arresto anomalo si verificava a causa di una chiamata di funzione su un puntatore condiviso Null (auditudeSettings). È stato aggiunto un controllo condizionale all&#39;interno di VideoEngineTimeline::placeToSourceTimeline() per assicurarsi che auditudeSettings siano disponibili prima di richiamare qualsiasi elemento su tale oggetto.
* ZD #32584 - Impossibile accedere alle informazioni complete presenti nel nodo &lt;Extensions> di una risposta VAST.
   * È stato risolto il problema relativo all&#39;analisi XML e ora NetworkAdInfo fornisce le informazioni complete presenti nel nodo &lt;Extensions>.
* ZD #35086 - Non è possibile ottenere dati di estensione completi dal lettore in caso di risposte VMAP specifiche.
   * Il problema era specifico per l&#39;estensione xml in quanto l&#39;analisi XML non funzionava se l&#39;estensione xml conteneva doppie virgolette nel valore dell&#39;attributo. È stato risolto il problema.

**Android TVSDK 2.5.4**

* ZenDesk#33659 - Sessione di riproduzione che abilita il debug remoto della visualizzazione Web.
   * WebViewDebbuging è impostato su False per impostazione predefinita. Per abilitare il debugging, impostare come true tramite l&#39;applicazione utilizzando setWebContentsDebuggingEnabled(true).
* ZenDesk#33011 - La timeline dell&#39;annuncio non è risolta in caso di richiesta CRS non riuscita.
   * Quando una richiesta CRS a un annuncio non riesce, la timeline viene risolta e vengono riprodotti gli annunci rimanenti.
* ZenDesk#34528 - La risoluzione video non viene aggiornata oltre 640x360 su un dongle di terza generazione di FireTV.
   * La risoluzione video si attiva quando si commuta il bit rate.
* ZenDesk#33192 - AudioTrack ha un nome null quando la traccia viene recuperata tramite AudioUpdatedEventListener::onAudioUpdated.
   * In alcuni scenari su FireTV Stick, l&#39;evento onAudioUpdate veniva attivato quando non si verificava alcun aggiornamento audio effettivo. Questo è stato corretto ora.

**Android TVSDK 2.5.3**

* Zendesk#32216 - TimedMetadata l&#39;iscrizione tag personalizzata non funziona.
   * Stiamo restituendo dati ID3 come array di byte (per supportare dati APIC o generici) al client, mentre in 1.4 stringa di restituzione. L&#39;array di byte non gestisce il carattere con terminazione null, pertanto mostrava al client un carattere speciale. Questo problema è stato risolto ora.
* Zendesk#32670 - Lettore che non arriva alla sequenza di riproduzione ridondante
   * Questo funziona correttamente ora e setNetworkDownVerificationUrl funziona come previsto.
* Zendesk#32369 - I sottotitoli codificati mostrano elementi di immondizia o artefatti a colori diversi.
   * È stato risolto il problema relativo ai problemi CC nell&#39;ultima build
* Zendesk#25590 - Miglioramento: TVSDK cookie store (da C++ a JAVA)
   * Android TVSDK ora supporta l&#39;accesso ai cookie tra il livello JAVA (memorizzato in CookieStore dell&#39;applicazione Android) e il livello TVSDK C++.
* Zendesk#32252 - TVSDK_Android_2.5.2.12 non sembra avere la correzione per PTPLAY-20269Questo problema è stato risolto e integrato nel ramo 2.5.2.
* Zendesk#31806 - I bastoncini di Auditude in PREPARINGPlayer si bloccavano nello stato Preparazione perché il codice xml di risposta aveva un tag vuoto. Ora il problema è stato risolto.
* Zendesk#31727 - I caratteri di sottotitoli codificati TVSDK 2.5 vengono ignorati o visualizzati in modo errato.
   * Il problema è stato risolto e non vengono rilasciati/visualizzati errori di battitura.
* Zendesk#31485 - DrmManager in 2.5
   * Si è verificato un problema nella creazione di DrmManager tramite il nuovo DrmManager(Context context). Implementata la classe DRMService che fornisce DRMManager.
* Streaming di risoluzione Zendesk#32794-1080P non riprodotto su Android.
   * Abbiamo modificato i metodi SizeAvailableEvent e Precedentemente getHeight() e getWidth() di SizeAvailableEvent in 2.5, utilizzati per restituire l&#39;altezza e la larghezza del frame, che sono stati restituiti dal formato multimediale. Ora restituisce rispettivamente l&#39;altezza e la larghezza di output restituiti dal decoder.
* Arresti anomali di Flash Player per Zendesk #19359 a causa della posizione dell&#39;attributo #EXT-X-FAXS-CM nel manifesto a livello di set.
   * Il tag #EXT-X-FAXS-CM deve essere sempre visualizzato nella playlist principale prima che singoli bitrate o segmenti vengano visualizzati nella playlist.

**Android TVSDK 2.5.2**

* Zendesk#17305 Artefatti in didascalie con sfondo non opaco.
setTreatSpaceAsAlphaNum in TextFormat è esposto. Per impostazione predefinita, la proprietà è False. Impostate la proprietà su True in un client per risolvere il problema di spazio vuoto.

* Zendesk#25097 con display CC offre artefatti visivi con impostazioni CC.
setTreatSpaceAsAlphaNum in TextFormat è esposto. Per impostazione predefinita, la proprietà è False. Impostate la proprietà su True in un client per risolvere il problema di spazio vuoto.

* La stringa agente Zendesk #31620 dell&#39;agente utente che esce dal lettore TVSDK è troncata.
La stringa agente utente non verrà più troncata dopo 128 caratteri.
La stringa di versione di Adobe Primetime viene aggiunta all&#39;agente utente del sistema.

* Zendesk #30809 L&#39;evento SEEK_END mancante impedisce la transizione dell&#39;app a uno stato di riproduzione.
* Il colore &#39;Cyan&#39; dei sottotitoli codificati Zendesk #30415 è ora più scuro del blu (turchese) rispetto alle precedenti versioni TVSDK di Primetime.

   Il colore viene cambiato da DarkCyan a Cyan.

* Zendesk #30727 Gli annunci VOD non vengono scaricati/risolti.

   In VMAP XML se è presente un tag VAST vuoto senza un tag di chiusura esplicito (‘&lt;/VAST>&#39;) e senza un carattere di nuova riga dopo di esso, l&#39;XML VMAP non viene analizzato correttamente e gli annunci potrebbero non essere riprodotti.

**Android TVSDK 2.5.1**

* arresto anomalo specifico del dispositivo (Samsung Galaxy Tab 4); VOD DRM LBA con Auditude e clicca su annunci.
* VHL - Le chiamate heartbeat errate vengono inviate quando si inizia il contenuto da un offset.
* Quando vengono riprodotti gli annunci VPAID, mancano le chiamate heartbeat VHL per event:type:play ad.
* Dopo aver impostato lo stato COMPLETE, il lettore torna allo stato PLAYING con SKIP adBreakPolicy per gli annunci post-roll.
* I cookie non vengono allegati alle callback di annunci in uscita.
* I cue point Ads non sono visibili.
* HLS con traccia SAP EAC3 separata non verrà caricato.
* Il lettore si arresta in modo anomalo quando TVSDK riceve un intento di attivazione dello schermo dopo il ripristino di Media Player.

## Problemi noti e limitazioni {#known-issues-and-limitations}

**Android TVSDK 2.7**

* TVSDK 2.7 supporta la risoluzione simultanea fino a 5 annunci.
* Nel caso della risposta VMAP, le chiamate Ad in un&#39;unica interruzione Ad vanno contemporaneamente, e le interruzioni Ad vengono risolte in sequenza.
* Nel caso di FER, le chiamate Ad in ogni opportunità vengono risolte contemporaneamente.

### Problemi noti e limitazioni delle versioni precedenti{#known-issues-limitations-previous-releases}

**Android TVSDK 2.5.6**

* Più interruzioni di annunci VMAP allo stesso tempo non sono supportate.

**Android TVSDK 2.5.3**

Questa versione presenta i seguenti problemi:

* La riproduzione di video live potrebbe presentare problemi di sincronizzazione audio-video su dispositivi di fascia bassa o condizioni di rete scadenti.
* Per i flussi FER, VirtualTime e localTime possono essere diversi. Anche FER con offset non funziona.
* La riproduzione potrebbe bloccarsi quando si ricercano contenuti audio di rilegatura tardiva.
* In modo intermittente, i sottotitoli WebVTT potrebbero non essere sincronizzati per i contenuti Live.
* La riproduzione rapida di pochi fotogrammi può essere vista in modo intermittente dopo l&#39;uscita da un&#39;interruzione pubblicitaria.
* A volte, l&#39;errore 303 viene generato per Tripple Wrapper Ad Breaks, anche se Ads sono riprodotti.

**Android TVSDK 2.5.2**

Questa versione presenta i seguenti problemi:

* La riproduzione video live potrebbe presentare problemi di sincronizzazione audio-video sui dispositivi di fascia bassa.
* La riproduzione può arrestarsi a volte quando si cerca di terminare il supporto VOD.
* Per i flussi FER, VirtualTime e localTime possono essere diversi. Inoltre, FER con offset non funziona.

**Android TVSDK 2.5.1**

Questa versione di TVSDK presenta i seguenti problemi:

* La riproduzione di video live potrebbe presentare problemi di sincronizzazione audio-video sui dispositivi di fascia bassa.
* Per i flussi FER, VirtualTime e localTime possono essere diversi. Inoltre, FER con offset non funziona.
* In VMAP XML, se è presente un tag VAST vuoto senza un tag di chiusura esplicito (&lt;/VAST>) e senza una nuova riga dopo di esso, il file XML VMAP non viene analizzato correttamente e gli annunci potrebbero non essere riprodotti.
* I post-roll VPAID non sono supportati.

## Risorse utili {#helpful-resources}

* [Requisiti di sistema](https://docs.adobe.com/content/help/en/primetime/programming/tvsdk-2-7-for-android/overview/c-psdk-android-2_7-requirements.html)
* [Guida di TVSDK 2.7 per programmatori Android](https://docs.adobe.com/content/help/en/primetime/programming/tvsdk-2-7-for-android/overview/c-psdk-android-2_7-overview-prod-audience-guide.html)
* [TVSDK Android Javadoc per API Reference](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.7/index.html)
* [Documento](https://help.adobe.com/en_US/primetime/api/psdk/cpp/namespaces.html) API TVSDK Android C++ - Ogni classe Java ha una classe C++ corrispondente, e la documentazione C++ contiene più materiale esplicativo rispetto a Javadocs, pertanto consulta la documentazione C++ per una migliore comprensione dell&#39;API Java.
* [Guida alla migrazione a TVSDK da 1.4 a 2.5 per Android (Java)](https://helpx.adobe.com/primetime/migration-guides/tvsdk-14-25-android.html)
* Per gestire gli scenari di attivazione/disattivazione della schermata, vedete il `Application_Changes_for_Screen_On_Off.pdf` file incluso nella build.
* Consulta la documentazione completa della guida nella pagina Informazioni e supporto [di](https://helpx.adobe.com/support/primetime.html) Adobe Primetime.