---
title: Note sulla versione di TVSDK 3.15 per Android
description: Le note sulla versione di TVSDK 3.15 per Android descrivono le novità o le modifiche, i problemi risolti e noti e i problemi del dispositivo in TVSDK Android 3.15
products: SG_PRIMETIME
topic-tags: release-notes
exl-id: cd2c64ef-dd42-4dc2-805f-eeb64a8a53d9
source-git-commit: 3b051c3188c81673129e12dfeb573aaf85c15c97
workflow-type: tm+mt
source-wordcount: '5516'
ht-degree: 0%

---

# Note sulla versione di TVSDK 3.15 per Android {#tvsdk-for-android-release-notes}

Le note sulla versione di TVSDK 3.15 per Android descrivono le novità o le modifiche, i problemi risolti e noti e i problemi del dispositivo in TVSDK Android 3.15.

Il lettore di riferimento Android è incluso con Android TVSDK nella directory samples/ della distribuzione. Il file README.md associato spiega come creare il lettore di riferimento.

>[!NOTE]
>
>Per creare correttamente il lettore di riferimento, come descritto nel file README.md distribuito con la versione, assicurati di effettuare le seguenti operazioni:
>
>1. Scarica VideoHeartbeat.jar da [https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases](https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases) (Libreria VideoHeartbeat per Android v2.0.0)
>1. Estrai VideoHeartbeat.jar nella cartella libs/.


TVSDK per Android offre molti miglioramenti delle prestazioni rispetto alle versioni precedenti. Offre un’esperienza visiva di alta qualità e dispone di tutte le funzioni della versione 1.4, ad eccezione del supporto Multi-CDN.

Il set completo di funzioni supportate e non supportate è presentato nel [Matrice di funzioni](#feature-matrix) sezione delle note sulla versione.

## Android TVSDK 3.15

Questa versione risolve il problema relativo agli arresti anomali dell’applicazione più volte quando manca il tag creativo o quando [!UICONTROL url CDATA] è vuoto in [!UICONTROL VAST] risposta.

Per informazioni sulle correzioni di bug in questa e nelle versioni precedenti, consulta [problemi risolti in TVSDK per Android](#resolved-issueszd).

### Nuove funzioni e miglioramenti nelle versioni precedenti

**Android TVSDK 3.14**

Questa versione risolve il problema di arresto anomalo dell’applicazione quando [!UICONTROL CDATA] il nodo è vuoto per qualsiasi [!UICONTROL ClickTracking], [!UICONTROL CustomClick] o [!UICONTROL CompanionClickTracking] elementi nella risposta VAST.

**Android TVSDK 3.13**

Lo streaming DRM widevine blocca o mostra i fotogrammi neri sullo switch ABR dei dispositivi FireTV, che includono i dispositivi Fire TV di 3a generazione Pendant e Fire TV Cube di 1a e 2a generazione.

Per risolvere il problema, imposta l’API `MediaPlayer.flushVideoDecoderOnHeaderChange(true)` per i dispositivi Fire TV specificati prima di avviare la riproduzione. Il valore predefinito è false.

**Android TVSDK 3.12**

Aggiornamento della versione gradle dell’applicazione Primetime Reference alla versione 5.6.4.

Per impostare ed eseguire l&#39;app Reference tramite Android Studio, segui le istruzioni del file ReadMe disponibile con TVSDK zip all&#39;indirizzo `TVSDK_Android_x.x.x.x/samples/PrimetimeReference/src/README.md`.

I principali problemi risolti dai clienti nella versione corrente sono menzionati in [problemi risolti](#resolved-issues) sezione.

**Android TVSDK 3.11**

* **Recupero della casella PSSH consentito** - TVSDK consente di recuperare la casella di intestazione specifica del sistema di protezione associata alla risorsa multimediale caricata corrente. Nuova API `getPSSH()` aggiunto a `com.adobe.mediacore.drm.DRMManager`.

Per ulteriori informazioni, consulta [DRM widevine](../programming/tvsdk-3x-android-prog/android-3x-content-security/android-3x-drm-widevine.md).

**Android TVSDK 3.10**

La versione si concentra sulla risoluzione dei principali problemi dei clienti, come menzionato in [problemi risolti](#resolved-issues) sezione.

**Android TVSDK 3.9**

* **Consegna sicura tramite HTTPS** - Android TVSDK 3.9 ha introdotto le funzionalità di distribuzione sicura tramite HTTPS per distribuire i contenuti in modo sicuro con scalabilità e prestazioni senza precedenti.

   Per abilitare la consegna sicura tramite HTTPS, è stata introdotta una nuova API in `NetworkConfiguration` classe.

   `public void setForceHTTPS (boolean value)`

   `public boolean getIsForceHTTPS()`

**Android TVSDK 3.8**

* **Supporto pre-roll con funzione Ad-Break parziale** - Con questo miglioramento, TVSDK 3.8 supporta gli annunci pre-roll con funzione di interruzione annuncio parziale (PABI).

L’annuncio pre-roll, se disponibile, viene riprodotto, quindi il contenuto viene riprodotto dal punto in diretta, emulando l’esperienza della televisione in diretta.

**Android TVSDK 3.7**

* Per il contenuto di prova Widevine, una nuova API `setMediaDrmCallback` nella classe DRMManager è esposto per sostituire l&#39;implementazione predefinita dell&#39;interfaccia MediaDrmCallback.

   `public static void setMediaDrmCallback(MediaDrmCallback callback)`

* È stato corretto l’errore AppCrash per la mancata gestione di `MediaPlayerEvent.ITEM_UPDATED` nel livello C++ (Android 64 bit).

**Android TVSDK 3.6**

* **Ottimizza le tue app per soddisfare i requisiti di 64 bit** - La libreria nativa `(libAVEAndroid.so)` è ora aggiornato e reso disponibile in due versioni. La posizione della libreria nativa armeabi (32 bit) esistente è stata modificata da `/framework/Player to /framework/Player/armeabi` e un&#39;ulteriore libreria arm64-v8a (64 bit) è introdotta in `/framework/Player/arm64-v8a.`

**Versione 3.5**

* **Just In Time Ad Resolution** - TVSDK 3.5 rimuove il supporto degli annunci riprodotti dalla timeline.

* **Abilitazione del supporto per la riproduzione offline** - Grazie alla riproduzione offline, gli utenti possono ora scaricare contenuti video sui propri dispositivi e guardarli quando non sono connessi. Per informazioni dettagliate, consulta &quot;[Riproduzione offline con Android](https://helpx.adobe.com/content/dam/help/en/primetime/programming-guides/psdk_android_3.5.pdf).&quot;

**Versione 3.4**

* TVSDK ora supporta la riproduzione di flussi CMAF per flussi CBC crittografati e semplici.

**Versione 3.3**

* **Modifiche API**

   * Viene aggiunta una nuova API a `NetworkConfiguration::setNumOfTimesManifestRetryBeforeError(n)*` per gestire errori di rete e timeout.
      * dove (n) è il numero di nuovi tentativi.

**Versione 3.2**

* **Supporto per risoluzione annunci paralleli e download di manifesti**

   * TVSDK 3.2 supporta la risoluzione simultanea, invece della risoluzione sequenziale per tutte le richieste e le interruzioni dell’annuncio eccetto VMAP.

   * Tutti i manifesti pubblicitari in un’interruzione pubblicitaria vengono scaricati contemporaneamente.

* **Abilitazione del supporto per la risoluzione degli annunci e il timeout del download del manifesto.**

   * Gli utenti possono ora impostare il valore di timeout per la risoluzione complessiva degli annunci e i download dei manifesti.  Nel caso di VMAP, il valore di timeout si applica per singole interruzioni pubblicitarie in quanto tutte le interruzioni pubblicitarie vengono risolte in sequenza.

* **Sono state introdotte nuove API nella classe AdvertisingMetadata:**

   * `void setAdResolutionTimeout(int adResolutionTimeout)`

   * `int getAdResolutionTimeout()`

   * `void setAdManifestTimeout(int adManifestTimeout)`

   * `int getAdManifestTimeout()`

* **API di seguito rimosse dalla classe AdvertisingMetadata:**

   * `void setAdRequestTimeout(int adRequestTimeout)`

   * `int getAdRequestTimeout()`

* **Abilitazione della riproduzione dei flussi con codec audio AC3/EAC3**

   * `void alwaysUseAC3OnSupportedDevices(boolean val)` in `MediaPlayer` classe

* **TVSDK supporta la riproduzione CMAF e plain stream per il CTR widevine crittografato.**

* **È ora supportata la riproduzione di flussi HEVC 4K.**

* **Richieste parallele di annunci pubblicitari** - TVSDK ora preacquisisce 20 richieste di chiamate di annunci in parallelo.

**Versione 3.0**

* **TVSDK 3.0 supporta i flussi HEVC (High Efficiency Video Coding).**

* **Just in Time - Risoluzione degli annunci più vicini ai marcatori degli annunci**
La funzione Lazy Ad Resolving risolve ora ogni interruzione pubblicitaria in modo indipendente. In precedenza, la risoluzione degli annunci era basata su un approccio in due fasi: i pre-roll venivano risolti prima dell’inizio della riproduzione e tutti gli slot mid/post roll venivano combinati dopo l’avvio della riproduzione. Con questa funzione avanzata, ogni interruzione pubblicitaria ora viene risolta in un momento specifico prima del punto di cue dell’annuncio.

>[!NOTE]
>
>La funzione Lazy Ad Resolving è ora modificata per essere disattivata per impostazione predefinita e deve essere abilitata esplicitamente.

Viene aggiunta una nuova API a `AdvertisingMetadata::setDelayAdLoadingTolerance` per ottenere la tolleranza al caricamento ritardato degli annunci associata a questi metadati pubblicitari.\
La ricerca è ora consentita subito dopo la PREPARAZIONE, la ricerca oltre le interruzioni pubblicitarie si tradurrà in una risoluzione immediata prima del completamento della ricerca.\
Modalità di segnalazione `SERVER_MAP` e `MANIFEST_CUES` sono supportati.

Per ulteriori informazioni, consulta [Guida per programmatori di TVSDK 3.0 per Android](../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/c-lazy-ad-resolving/c-lazy-ad-resolving.md) su modifiche all’API e agli eventi.

* **Aggiornato `targetSdkVersion` alla versione più recente**

Aggiornato `targetSdkVersion` da 19 a 27 per il corretto funzionamento.

* **Placement.Type getPlacementType() è ora un metodo su TimelineMarker dell’interfaccia**

   Questo metodo restituirà un tipo di posizionamento Placement.Type.PRE_ROLL, Placement.Type.MID_ROLL o Placement.Type.POST_ROLL. Se un’interruzione pubblicitaria non è stata risolta, il metodo getDuration() nell’interfaccia TimelineMarker restituirà 0.

**Versione 2.5.6.**

* **TVSDK 2.5 supporta Android P.**

* **Abilitazione dell&#39;audio in background**

   Per abilitare la riproduzione audio quando l’app si sposta dal primo piano in background, l’app deve chiamare `enableAudioPlaybackInBackground` API di MediaPlayer con argomento true come quando il lettore è nello stato PREPARATO.

* **alwaysUseAudioOutputLatency(valore booleano) nella classe MediaPlayer**

Se questa opzione è impostata, utilizzate la latenza di output nel calcolo della marca temporale audio.
Valore dei parametri booleani: True per utilizzare la latenza di output audio nel calcolo della marca temporale audio.

* **Ottimizzato per ottenere la migliore esperienza di riproduzione anche se la velocità della larghezza di banda diminuisce improvvisamente**

TVSDK ora annulla il download del segmento in corso, se necessario, e passa dinamicamente alla rappresentazione appropriata. Ciò avviene passando senza interruzioni tra i bitrate.

**Versione 2.5.5**

* **Inserimento interruzione annuncio parziale**

   Esperienza simile alla TV, ovvero partecipare nel mezzo di un annuncio senza attivare il tracciamento dell’annuncio parzialmente guardato.\
   Esempio: l’utente si unisce al centro (a 40 secondi) di un’interruzione pubblicitaria di 90 secondi composta da tre annunci di 30 secondi. Questo è a 10 secondi dal secondo annuncio nell’interruzione.

   * Il secondo annuncio viene riprodotto per la durata rimanente (20 secondi) seguito dal terzo annuncio.

   * I tracker degli annunci per l’annuncio parziale riprodotto (secondo annuncio) non vengono attivati. I tracker solo per il terzo annuncio vengono sparati.

* **Caricamento sicuro degli annunci tramite HTTPS**

   Adobe Primetime fornisce un’opzione per richiedere la prima chiamata a primetime ad server e CRS su https.

* **AdSystem e ID creativo aggiunti alle richieste CRS**

   Ora inclusi `AdSystem` e `CreativeId` come nuovi parametri nelle richieste 1401 e 1403.

* **SetEncodeUrlForTracking API nella classe NetworkConfiguration rimossa** come i caratteri non sicuri in un URL devono essere codificati.

**Versione 2.5.4**

Android TVSDK v2.5.4 offre i seguenti aggiornamenti e modifiche API:

* Modifiche nel valore predefinito per `WebViewDebbuging`

   `WebViewDebbuging` valore impostato su `Fals`e per impostazione predefinita. Per abilitarlo, chiama `setWebContentsDebuggingEnabled(true)` nell&#39;applicazione.

* **Aggiornamento delle versioni OpenSSL e Curl**

   libcurl è stato aggiornato alla versione v7.57.0 e OpenSSL alla versione v1.0.2k.

* Accesso a livello di app per l’oggetto di risposta VAST

   Presentata una nuova API `NetworkAdInfo::getVastXml()` che fornisce all’applicazione l’accesso all’oggetto di risposta VAST.

**Versione 2.5.3**

Android TVSDK v2.5.3 offre i seguenti aggiornamenti e modifiche API.

* Tutti i clienti TVSDK che utilizzano CRS sono invitati ad aggiornare le loro app con TVSDK 2.5.3.85 o versione più recente su Android. Si tratterà di una sostituzione a cascata dell’implementazione dell’app esistente. Dopo l’aggiornamento di TVSDK, controlla le richieste dell’URL creativo di CRS in uno strumento proxy (ad esempio, Charles) e conferma che il nome host e la versione nel percorso riflettano come nella struttura dell’URL di esempio riportata di seguito.

   `https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784 bf3586d.m3u8`

* Agente utente di TVSDK personalizzabile: sono state aggiunte alcune nuove API per personalizzare gli agenti utente.

   * `setCustomUserAgent(String value)`
   * `getCustomUserAgent()`

* Condivisione di cookie tra l&#39;applicazione Android e TVSDK: Android TVSDK ora supporta l&#39;accesso di cookie tra il livello JAVA (memorizzato in CookieStore dell&#39;applicazione Android) e il livello C++ TVSDK. Ora è possibile impostare e/o modificare i cookie nel livello C++ nativo in quanto verranno esposti all’archivio dei cookie Java.

* Modifiche API:

   * Un nuovo evento `CookiesUpdatedEvent` viene aggiunto. Viene inviato dal lettore multimediale quando il relativo cookie viene aggiornato.

   * Viene aggiunta una nuova API a `NetworkConfiguration::set/ getCustomUserAgent()` per utilizzare l’agente utente personalizzato.

   * Viene aggiunta una nuova API a `NetworkConfiguration::set/ getEncodedUrlForTracking` per forzare la codifica dei caratteri non sicuri.

   * Viene aggiunta una nuova API a `NetworkConfiguration::getNetworkDownVerificationUrl()` per impostare un URL di verifica della rete in caso di failover.

   * Viene aggiunta una nuova proprietà a `TextFormat::treatSpaceAsAlphaNum` che definiscono se trattare lo spazio come alfanumerico durante la visualizzazione dei sottotitoli.

* Modifiche in `SizeAvailableEvent`. Precedentemente, `getHeight()` e `getWidth()` metodi di `SizeAvailableEvent` nella versione 2.5.2 veniva utilizzata per restituire l’altezza e la larghezza del frame restituite dal formato multimediale. Ora restituisce rispettivamente l&#39;altezza e la larghezza di output restituite dal decodificatore.

* Modifiche nel comportamento di buffering: il comportamento di buffering è cambiato. Spetta allo sviluppatore di app decidere cosa fare in caso di buffer vuoto. 2.5.3 utilizza le dimensioni del buffer di riproduzione in una situazione di buffer vuoto.

**Versione 2.5.2**

Android TVSDK v2.5.2 offre importanti correzioni di bug e alcune modifiche API.

**Versione 2.5.1**

Le nuove importanti funzioni rilasciate in Android 2.5.1.

* **Miglioramenti delle prestazioni -** La nuova architettura TVSDK 2.5.1 offre diversi miglioramenti delle prestazioni. In base alle statistiche di uno studio di benchmarking di terze parti, la nuova architettura offre una riduzione del tempo di avvio di 5 volte e un numero di fotogrammi saltati di 3,8 volte inferiore rispetto alla media del settore:

* **Attivazione immediata per VOD e live -** Quando attivate l&#39;opzione di attivazione immediata, TVSDK inizializza e memorizza in buffer i contenuti multimediali prima dell&#39;avvio della riproduzione. Poiché è possibile avviare più istanze MediaPlayerItemLoader contemporaneamente in background, è possibile eseguire il buffer di più flussi. Quando un utente cambia il canale e il flusso viene memorizzato correttamente nel buffer, la riproduzione sul nuovo canale inizia immediatamente. TVSDK 2.5.1 supporta anche l&#39;opzione di attivazione immediata per **live** flussi anche. I flussi live vengono riinseriti nel buffer quando la finestra live si sposta.

* **Logica ABR migliorata -** La nuova logica ABR si basa sulla lunghezza del buffer, sul tasso di variazione della lunghezza del buffer e sulla larghezza di banda misurata. Questo assicura che l&#39;ABR scelga il bit rate corretto quando la larghezza di banda fluttua e ottimizza anche il numero di volte che l&#39;interruttore di bitrate si verifica effettivamente monitorando la velocità con cui cambia la lunghezza del buffer.

* **Download/Sottosegmentazione segmento parziale -** TVSDK riduce ulteriormente le dimensioni di ciascun frammento per iniziare la riproduzione il prima possibile. Il frammento ts deve avere un fotogramma chiave ogni due secondi.

* **Risoluzione annuncio lazy -** TVSDK non attende la risoluzione degli annunci non preroll prima di avviare la riproduzione, riducendo in tal modo il tempo di avvio. API come seek e trick-play non sono ancora consentite fino a quando tutti gli annunci non sono risolti. Questo è applicabile ai flussi VOD utilizzati con CSAI. Operazioni come ricerca e avanzamento rapido non sono consentite fino al completamento della risoluzione dell’annuncio. Per i flussi live, questa funzione non può essere abilitata per la risoluzione degli annunci durante un evento live.

* **Connessioni di rete persistenti -** Questa funzione consente a TVSDK di creare e memorizzare un elenco interno di connessioni di rete persistenti. Queste connessioni vengono riutilizzate per più richieste, anziché aprire una nuova connessione per ogni richiesta di rete e quindi eliminarla in seguito. Ciò aumenta l’efficienza e diminuisce la latenza nel codice di rete, con conseguente miglioramento delle prestazioni di riproduzione.
Quando TVSDK apre una connessione chiede al server di *keep-alive* connessione. Alcuni server potrebbero non supportare questo tipo di connessione, nel qual caso TVSDK tornerà a effettuare una connessione per ogni richiesta. Inoltre, anche se le connessioni persistenti sono attive per impostazione predefinita, TVSDK ora dispone di un&#39;opzione di configurazione che consente alle app di disattivare le connessioni persistenti, se necessario.

* **Download parallelo -** Il download di video e audio in parallelo anziché in serie riduce i ritardi di avvio. Questa funzione consente la riproduzione di file HLS Live e VOD, ottimizza l&#39;utilizzo della larghezza di banda disponibile da un server, riduce la probabilità di entrare in situazioni di buffer underrun e riduce al minimo il ritardo tra il download e la riproduzione.

* **Download paralleli di annunci -** TVSDK preacquisisce gli annunci in parallelo alla riproduzione del contenuto prima che l’annuncio venga interrotto, consentendo in tal modo una riproduzione fluida di annunci e contenuti.

* **Riproduzione**

* **Riproduzione di contenuti MP4 -** Non è necessario ripetere la trascodifica dei clip MP4 brevi per la riproduzione in TVSDK.

   >[!NOTE]
   >
   >La commutazione ABR, la riproduzione mediante trick, l&#39;inserimento di annunci, l&#39;associazione audio in ritardo e la sottosegmentazione non sono supportate per la riproduzione MP4.

* **Riproduzione &quot;trrick&quot; con velocità bit adattiva (ABR) -** Questa funzione consente a TVSDK di passare da un flusso iFrame a un altro in modalità &quot;trick play&quot;. È possibile utilizzare profili non iFrame per eseguire la riproduzione a velocità inferiori.

* **Gioco più fluido -** Questi miglioramenti migliorano l’esperienza utente:

   * Bit rate adattivo e selezione del frame rate durante la riproduzione dei &quot;trick&quot;, in base alla larghezza di banda e al profilo del buffer

   * Utilizzo dello streaming principale invece dello streaming IDR per una riproduzione rapida fino a 30 fps.

* **Protezione dei contenuti**

   * **Protezione dell&#39;output basata sulla risoluzione -** Questa funzione associa le restrizioni di riproduzione a risoluzioni specifiche, fornendo controlli DRM più dettagliati.

* **Supporto per flussi di lavoro**

   * **Integrazione fatturazione diretta -** In questo modo le metriche di fatturazione vengono inviate al backend di Adobe Analytics, certificato da Adobe Primetime per i flussi utilizzati dal cliente.

   TVSDK raccoglie automaticamente le metriche, rispettando il contratto di vendita del cliente per generare rapporti periodici sull&#39;utilizzo richiesti a scopo di fatturazione. In ogni evento di avvio del flusso, TVSDK utilizza l’API di inserimento dati di Adobe Analytics per inviare alla suite di rapporti di proprietà di Adobe Analytics Primetime metriche di fatturazione quali il tipo di contenuto, i flag con inserimento di annunci e i flag con drm abilitato, in base alla durata del flusso fatturabile. Questo non interferisce con le suite di rapporti Adobe Analytics del cliente o non viene incluso nelle sue chiamate al server. Su richiesta, questo rapporto sull’utilizzo della fatturazione viene inviato periodicamente ai clienti. Questa è la prima fase della funzione di fatturazione che supporta solo la fatturazione dell’utilizzo. Può essere configurato in base al contratto di vendita utilizzando le API descritte nella documentazione. Questa funzione è attivata per impostazione predefinita. Per disattivare questa funzione, consulta l’esempio del lettore di riferimento.

   * **Migliore supporto per il failover -** Sono state implementate strategie aggiuntive per continuare la riproduzione ininterrotta, nonostante gli errori dei server host, dei file delle playlist e dei segmenti.


* **Pubblicità**

   * **Integrazione Moat -** Supporto per la misurazione della visualizzabilità degli annunci da Moat.

   * **Banner -** I banner complementari vengono visualizzati accanto a un annuncio lineare e spesso continuano a essere visualizzati sulla visualizzazione al termine dell’annuncio. I banner possono essere di tipo html (snippet di HTML) o iframe (URL di una pagina iframe).

* **Analytics**

   * **VHL 2.0 -** Questa è la più recente integrazione ottimizzata della Video Heartbeat Library (VHL) per la raccolta automatica dei dati di utilizzo per Adobe Analytics. La complessità delle API è stata ridotta a per semplificare l’implementazione. Scarica la libreria VHL [v2.0.0 per Android](https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases) ed estrarre il file JAR nella cartella libs.

* **SizeAvaliableEventListener**

   * `getHeight()` e `getWidth()` metodi di `SizeAvailableEvent` ora restituisce l’output rispettivamente in altezza e larghezza. Le proporzioni di visualizzazione possono essere calcolate come segue:

      ```java
      SizeAvailableEvent e;
      DAR = e.getWidth()/ e.getHeight();
      ```

      Per calcolare la larghezza e l&#39;altezza del frame è inoltre possibile utilizzare il rapporto di formato di archiviazione in termini di larghezza e altezza del frame:

      ```java
      SAR = e.getSarWidth()/e.getSarHeight();
      frameHeight = e.getHeight();
      frameWidth = e.getWidth()/SAR;
      ```

* **Cookie**

   * Android TVSDK ora supporta l’accesso ai cookie JAVA memorizzati in CookieStore dell’applicazione Android. Viene fornita un’API di callback (onCookiesUpdated) per registrare ogni volta che un nuovo cookie arriva come parte di **Set-Cookie** Intestazione di risposta. Questi cookie sono disponibili come elenco di cookie HTTP utilizzati per un URI/dominio diverso impostando questi valori cookie su quel particolare URI/dominio utilizzando CookieStore. Allo stesso modo, i valori dei cookie in TVSDK vengono aggiornati utilizzando l’API di aggiunta CookieStore.

## Matrice di funzioni {#feature-matrix}

TVSDK per Android supporta una serie di funzioni che è possibile implementare per aggiungere funzionalità alle applicazioni video.

Nelle tabelle delle funzioni riportate di seguito, una &quot;Y&quot; indica che la funzione è supportata nella versione corrente.

| Funzionalità | Tipo di contenuto | HLS |
|---|---|---|
| Riproduzione generale (riproduzione, pausa, ricerca) | VOD + Live | Y |
| FER - Riproduzione generale (riproduzione, pausa, ricerca) | VOD FER | Y |
| Ricerca durante la riproduzione di un annuncio | VOD + Live | Non supportato |
| Riproduzione HEVC | VOD + Live | Solo contenitore fMP4 |
| AC3 ed EAC3 | VOD + Live | Non supportato |
| MP3 | VOD | Non supportato |
| Riproduzione di contenuti MP4 | VOD | Y |
| Logica di commutazione del bit rate adattivo | VOD + Live | Y |
| Riproduzione solo audio | VOD + Live | Y |
| Supporto di più reti CDN | VOD + Live | Non supportato |
| Riproduzione di annunci con contenuti multimediali solo audio | VOD + Live | Non supportato |
| Sottotitoli codificati - 608/708 | VOD + Live | Y |
| Sottotitoli codificati - WebVTT | VOD + Live | Y |
| Failover del manifesto | VOD + Live | Y |
| Failover avanzato | VOD + Live | Y |
| Notifiche QoS e lettore | VOD + Live | Y |
| Supporto per le intestazioni dei cookie | VOD + Live | Y |
| Supporto per intestazioni HTTP personalizzate | VOD + Live | Y (obbligatorio inserire nell’elenco Consentiti) |
| Impostare i parametri di controllo del buffer | VOD + Live | Y |
| Impostazione dei controlli del bit rate adattivo | VOD + Live | Y |
| Tag manifesto personalizzati | VOD + Live | Y |
| Late Audio Binding | VOD + Live | Y |
| Reindirizzamento 302 | VOD + Live | Y |
| Riproduzione con offset | VOD + Live | Y |
| Trick Play | VOD + Live | Y |
| Slow motion in Trick Play | VOD + Live | Non supportato |
| Smooth Trick Play (con ABR) | VOD + Live | Y |
| Analisi ID3 | VOD + Live | Y |
| Sospensione attività degli annunci | VOD + Live | Non supportato |
| Istantanea attiva | VOD + Live | Non supportato |
| Supporto per marcatori di discontinuità | VOD + Live | Y |
| 302 Adesività reindirizzamento | VOD + Live | Y |

| Funzionalità | Tipo di contenuto | HLS |
|---|---|---|
| Riproduzione generale, annunci abilitati | VOD + Live | Y |
| Contenuto FER con annunci abilitati | VOD | Y |
| Comportamenti predefiniti degli annunci | VOD + Live | Y |
| VAST 2.0/3.0 | VOD + Live | Y |
| VMAP 1.0 | VOD + Live | Y |
| Annunci MP4 | VOD + Live | Y (da CRS) |
| Riproduzione nei trucchi con annunci abilitata | VOD + Live | Y |
| Solo annuncio | VOD | Y |
| Parametri di targeting | VOD + Live | Y |
| Parametri personalizzati | VOD + Live | Y |
| Comportamenti annuncio personalizzati | VOD + Live | Y |
| Tag annuncio personalizzati | Live | Y |
| Ad Resolver personalizzati | VOD + Live | Y |
| Ad Resolver personalizzato ruota libera | VOD | Y |
| C3 | VOD + Live | Non supportato |
| Risoluzione annuncio lazy | VOD | Y |
| Supporto per marker di discontinuità - SSAI | VOD + Live | Y |
| Annunci aziendali, annunci banner e annunci cliccabili | VOD + Live | Y |
| VPAID 2.0 | VOD + Live | Y (JS) |
| Uscita anticipata dall’annuncio | Live | Y |
| Priorità creativa basata su regole | VOD + Live | Y |
| Regole CRS | VOD + Live | Y |
| Ad Resolver JSON | VOD + Live | Non supportato |
| Integrazione Moat | VOD + Live | Y |
| Inserimento interruzione pubblicitaria parziale | Live | Y |

| Funzionalità | Tipo di contenuto | HLS |
|---|---|---|
| Crittografia AES | VOD + Live | Y |
| Esempio di crittografia AES | VOD + Live | Y |
| Flussi con token | VOD + Live | Y |
| DRM widevine | VOD + Live | Solo contenitore fMP4 |
| DRM Primetime | VOD + Live | Y |
| Riproduzione esterna (RBOP) | VOD + Live | Solo DRM di Primetime |
| Rotazione licenza | VOD + Live | Solo DRM di Primetime |
| Rotazione tasti | VOD + Live | Solo DRM di Primetime |

| Funzionalità | Tipo di contenuto | HLS |
|---|---|---|
| Integrazione Adobe Analytics VHL | VOD + Live | Y |
| Fatturazione | VOD + Live | Y |

## Problemi risolti {#resolved-issues}

Se la risoluzione è associata a un problema segnalato, viene visualizzato un riferimento Zendesk, ad esempio ZD#xxxxx.

**Android TVSDK 3.15**

Questa sezione fornisce un riepilogo del problema risolto nella versione Android di TVSDK 3.14.

* ZD#46903 - L’applicazione si arresta più volte quando manca il tag creativo o quando [!UICONTROL url CDATA] è vuoto in [!UICONTROL VAST] risposta.

**Android TVSDK 3.14**

* ZD#46903 - L’applicazione si blocca quando [!UICONTROL CDATA] il nodo è vuoto per qualsiasi [!UICONTROL ClickTracking], [!UICONTROL CustomClick] o [!UICONTROL CompanionClickTracking] elemento in [!UICONTROL VAST] risposta.

### Problemi risolti nelle versioni precedenti

**Android TVSDK 3.12**

* ZD#40584 - L’app Primetime Reference non viene generata con la versione più recente di gradle.

**Android TVSDK 3.11**

* ZD#41252 - Caratteri coreani in WebVTT interrotti dopo Android 7.1.

**Android TVSDK 3.10**

* ZD#40340 - L’applicazione si arresta in modo anomalo con l’errore &quot;App Not Responding&quot; (L’app non risponde) durante il tentativo di riproduzione dopo il blocco che elenca tutti i file TS (TypeScript).

**Android TVSDK 3.8**

* Nessun nuovo problema aggiunto.

**Android TVSDK 3.7**

* Nessun nuovo problema aggiunto.

**Android TVSDK 3.6**

* Nessun nuovo problema aggiunto.

**Versione 3.5**

* ZD#37503 - Le risposte JSON per le regole CRS vengono memorizzate nella cache per evitare le richieste duplicate.

**Versione 3.4**

* ZD#37996 - È stato risolto un problema relativo alla riproduzione irregolare di flussi HEVC CMAF lineari e VOD.
* ZD#37706 - È stato risolto un problema relativo ai sottotitoli illeggibili.
* ZD#37622 - È stato risolto un problema relativo a URIyntaxErrors irreversibili per annunci specifici.
* ZD#36938 - È stato risolto un problema relativo al passaggio del bitrate al bitrate medio e quindi al bitrate più alto dopo l’uscita dalle riproduzioni non autorizzate.

**Versione 3.3**

* ZD#37394 - L’avanzamento rapido della risorsa CMAF causa artefatti dopo i cambiamenti di velocità.
   * È stato risolto un problema che si verificava con una modifica del profilo durante la riproduzione con trucco.
* ZD#37396 - Mancano eventi di tracciamento degli annunci per alcuni mid-roll e post-roll.
   * È stato risolto un caso specifico relativo agli eventi di tracciamento degli annunci.
* ZD#37491 - Il codice di stato HTTP con meta di errore non è presente.
   * Lavorava sulla propagazione degli errori di rete più in alto nello stack.
* ZD#37808 - Elenco consentiti di nuova intestazione personalizzata.
   * Supporto di SSAI_TAG aggiunto come parte di questa correzione.
* ZD#37622 - Errori di sintassi URI da Ad Pod specifici.
   * È stato risolto un problema relativo all’arresto anomalo della riproduzione in streaming quando all’app Android del cliente vengono forniti annunci contenenti una percentuale non codificata
* ZD#37631 - Meccanismo di esecuzione di un nuovo tentativo del manifesto principale per Android TVSDK.
   * È stata aggiunta una nuova API nella configurazione di rete per la gestione di questo miglioramento. Se questa API non viene utilizzata, il manifesto non viene ritentato. Se viene utilizzato, il manifesto verrà ritentato per la gestione degli errori di rete e dei timeout.

**Versione 3.2**

* ZD#37493- I beacon di tracciamento per la riproduzione live non vengono attivati in modo intermittente per il primo annuncio in sequenza.
* ZD#36985- I beacon di tracciamento non vengono inviati per interruzioni pubblicitarie vuote nella risposta VMAP.
* ZD#37134 - TVSDK genera l’ID errato per la risposta VMAP in modo intermittente.

**Versione 3.0**

* ZD#33740 - TVSDK genera un avviso non necessario subito dopo la creazione di un oggetto MediaPlayer e la chiamata replaceCurrentResource()

   * È stata migliorata la correzione precedente chiamando Ripristina solo quando il lettore è in stato sospeso

* ZD#36442 - Ogni nuova riproduzione disconnette la sessione di debug remoto rendendo impossibile il debug.

   * Debug non possibile per impostazione predefinita nella visualizzazione Web in quanto il debug non è abilitato per impostazione predefinita. Se necessario, l’app deve abilitare il debug chiamando setWebContentsDebuggingEnabled(true) sull’oggetto restituito da MediaPlayer.getCustomAdView().

* ZD#33688 - Supporto per la risoluzione degli annunci Just In Time

   * Le interruzioni pubblicitarie vengono risolte a un intervallo specificato prima della posizione dell’interruzione pubblicitaria.

* ZD#36441 - La durata della finestra live continua ad aumentare oltre i 5 minuti causando diversi problemi.

   * È stato risolto un problema che causava l&#39;aggiunta di virtualStartTime due volte durante il calcolo del punto di attivazione virtuale.

**Android TVSDK 2.5.6**

* #34992 ZD - La lingua nei sottotitoli codificati è vuota.

   * È stato risolto un caso in cui TVSDK non stava analizzando #EXT-X-MEDIA:TYPE=CLOSED-CAPTIONS dal manifesto principale per ottenere i dettagli del tracciamento della didascalia.

* ZD #35078 - Convalida P per Android.

   * TVSDK 2..5.6 è stato convalidato con le build beta più recenti di Android P. Nessun problema trovato a causa del nuovo sistema operativo Android.

* #34149 ZD: il lettore continua a richiedere i manifesti anche se si verifica un errore.

   * È stato risolto il caso in cui TVSDK effettuava chiamate ripetitive anche quando tutti i profili non erano attivi (errore 404).

* ZD #31533 - Riproduzione di audio su Android dopo l’invio in background dell’app.

   * Aggiunto `enableAudioPlaybackInBackground` API di MediaPlayer che deve essere chiamata con &quot;True&quot; come argomento (quando il lettore è in stato READY) per abilitare la riproduzione di audio quando l’app è in background.

**Android TVSDK 2.5.5**

* ZD #21647 - Android TVSDK notifica 640x368 quando la dimensione video effettiva è 640x360.

   * A causa della variabile m_nOutputHeight (all’interno di AndroidMCVideoDecoder) che viene aggiornata con l’altezza del fotogramma invece dell’altezza di output effettiva. Sono state apportate modifiche rilevanti alla funzione getVideoFrame per calcolare correttamente m_nOutputHeight.

* ZD #26614 - Urgente: distribuzione di annunci di terze parti / programmatica: mancata distribuzione delle impression.

   * È stata migliorata la correzione precedente gestendo il caso nell’analisi XML in cui il problema era riproducibile quando &quot;spazio&quot; è prima del segno &quot;uguale a&quot; come &lt;vast version=&quot;2.0&quot;>

* ZD #29296 - Android: aggiungi AdSystem e Creative ID alle richieste CRS.

   * Ora inclusione di &quot;AdSystem&quot; e &quot;CreativeId&quot; come nuovi parametri nelle richieste 1401 e 1403.

* #33062 ZD - TVSDK si blocca al verificarsi del carattere di barra verticale nella risposta VAST sotto il nodo CDATA

   * SetEncodeUrlForTracking API nella classe NetworkConfiguration rimossa come caratteri non sicuri in un URL da codificare

* #33063 ZD: la logica di selezione del file CRS è stata interrotta. TVSDK non inviava richieste CRS per il formato webm, ma per i file 3gpp.

   * È stata corretta la logica. Quando si utilizzano file multimediali con formato webm e 3gpp, CRS richiede di essere inviato per webm. Quando si utilizzano entrambi i file multimediali in formato 3gpp, la richiesta CRS viene inviata per il file 3gpp con bitrate più elevato.

* ZD #33125 - L’app Android si blocca con un tag DoubleClick specifico all’interno della VMAP.

   * È stato risolto lo scenario per evitare l’arresto anomalo.

* #32256 ZD - Problema relativo alla rotazione delle licenze e alla rotazione dei tasti - Accesso Adobe

   * È stata corretta l’inizializzazione dei segmenti con i metadati DRM per il contenuto SampleAES. Compatibile con contenuti AES128.

* ZD #33619 - Avanzamento rapido di una playlist in crescita bloccata nello stato di buffering vicino a un punto live.

   * Ha gestito il caso quando ha attraversato il punto in diretta in modalità di gioco trick

* #34151 ZD - Oggetti TimedMetadata non ordinati.

   * Due eventi TimedMetadata venivano visualizzati in ordine casuale se appartenevano alla stessa ora nella timeline. Mantenuto l&#39;ordine originale nel manifesto.

* ZD #34189 - Problema durante la ricerca dell’inizio dell’interruzione pubblicitaria.

   * Il problema era con gli annunci SSAI che vengono uniti utilizzando la discontinuità. E la causa era un comportamento quando cerchiamo di iniziare queste pubblicità, cerchiamo un fotogramma chiave e non lo troviamo. Il motivo era che il timestamp audio minimo dell’annuncio era precedente al timestamp video minimo. Pertanto, finiamo per cercare un fotogramma chiave in un frammentoDati dump errato. Corretto ora.

* ZD #34528 - Risoluzione video non aggiornamento oltre 640x360 su FireTV 3a gen dongle.

   * Miglioramento della correzione per includere gli aggiornamenti firmware più recenti

* ZD #34793 - TVSDK 2.5.x utilizzava l’arresto anomalo con il risolutore dei contenuti personalizzato in alcuni casi in cui VideoEngine supponeva che le impostazioni di controllo dell’audience fossero disponibili e non lo fossero.

   * L’arresto anomalo era dovuto a una chiamata di funzione su un puntatore condiviso Null (auditudeSettings). È stato aggiunto un controllo condizionale in VideoEngineTimeline::placeToSourceTimeline() per verificare che auditudeSettings sia disponibile prima di richiamare qualsiasi elemento su tale oggetto.

* #32584 ZD - Impossibile accedere alle informazioni complete presenti nel &lt;extensions> nodo di una risposta VAST.

   * È stato risolto il problema relativo all&#39;analisi XML e ora NetworkAdInfo fornisce le informazioni complete presenti nel &lt;extensions> nodo

* ZD #35086 - Non si ottengono dati completi sull’estensione dal lettore in caso di risposte VMAP specifiche.

   * Il problema era specifico dell’estensione xml poiché l’analisi XML non funzionava se l’estensione xml conteneva virgolette doppie all’interno del valore dell’attributo. È stato risolto il problema.

**Android TVSDK 2.5.4**

* ZenDesk#33659 - Sessione di riproduzione che abilita il debug remoto di webview.

WebViewDebbuging è impostato su False per impostazione predefinita. Per abilitare il debug, impostare come true tramite l&#39;applicazione utilizzando setWebContentsDebuggingEnabled(true).

* ZenDesk#33011 - La timeline dell’annuncio non viene risolta in caso di richiesta CRS non riuscita.

   Quando una richiesta CRS a un annuncio non riesce, la timeline viene risolta e gli annunci rimanenti vengono riprodotti.

* ZenDesk#34528 - La risoluzione video non si aggiorna oltre 640x360 su dongle FireTV di terza generazione.

   La risoluzione video si attiva come commutatori della velocità di trasmissione.

* ZenDesk#33192 - AudioTrack ha un nome null quando il brano viene recuperato tramite AudioUpdatedEventListener::onAudioUpdated.

   In alcuni scenari su FireTV Stick, l&#39;evento onAudioUpdate veniva attivato quando non vi era alcun aggiornamento audio effettivo. Questo problema è stato risolto adesso.

**Android TVSDK 2.5.3**

* Zendesk#32216 - L’abbonamento tag personalizzato TimedMetadata non funziona.

   Stiamo restituendo i dati ID3 come una matrice di byte (per supportare dati APIC o generici) al client, mentre nella stringa restituita 1.4. L’array di byte non gestisce il carattere null terminated in sé, pertanto mostrava al client un carattere speciale. Questo problema è stato risolto adesso.
* Zendesk#32670 - Impossibile eseguire il failover del lettore sulla sequenza di riproduzione ridondante

   Questa operazione ora funziona correttamente e setNetworkDownVerificationUrl funziona come previsto.
* Zendesk#32369 - La didascalia mostra diversi colori di rifiuti o artefatti.

   Il problema relativo ai glitch CC è stato risolto nella build più recente
* Zendesk#25590 - Miglioramento: archivio cookie TVSDK ( da C++ a JAVA )

   Android TVSDK ora supporta l’accesso ai cookie tra il livello JAVA (memorizzato in CookieStore dell’applicazione Android) e il livello C++ TVSDK.
* Zendesk#32252 - TVSDK_Android_2.5.2.12 non sembra avere la correzione per PTPLAY-20269

   Questo problema è stato risolto e integrato nel ramo 2.5.2.
* Zendesk#31806 - Il pubblico si attacca alla PREPARAZIONE

   Il lettore si è bloccato in stato di preparazione perché l&#39;XML di risposta conteneva un tag vuoto. Ora il problema è risolto.
* Zendesk#31727 - I caratteri di sottotitoli codificati TVSDK 2.5 non vengono inseriti o contengono un errore di ortografia.

   Il problema è risolto e non verrà eliminato o digitato in modo errato alcun carattere.
* Zendesk#31485 - DrmManager in 2.5

   Si è verificato un problema nella creazione di DrmManager tramite il nuovo DrmManager (contesto di contesto). È stata implementata la classe DRMService che fornirebbe DRMManager.
* Zendesk#32794- Il flusso di risoluzione 1080P non viene riprodotto su Android

   Sono stati modificati i metodi SizeAvailableEvent e Precedentemente, getHeight() e getWidth() di SizeAvailableEvent in 2.5 utilizzati per restituire l’altezza e la larghezza del frame, restituite dal formato multimediale. Ora restituisce rispettivamente l&#39;altezza e la larghezza di output restituite dal decodificatore.
* Il Flash Player di #19359 Zendesk si blocca a causa della posizione di #EXT-X-FAXS-CM attributo nel manifesto a livello di set.

   Il tag #EXT-X-FAXS-CM deve sempre comparire nella playlist principale prima che singoli bitrate o segmenti vengano visualizzati nella playlist.

**Android TVSDK 2.5.2**

* Zendesk#17305 Artefatti in sottotitoli codificati con sfondo non opaco.

   La proprietà setTreatSpaceAsAlphaNum in TextFormat è esposta. Per impostazione predefinita, la proprietà è False. Impostare la proprietà su True in un client per risolvere il problema relativo allo spazio scuro.

* Lo schermo Zendesk#25097 CC presenta artefatti visivi con impostazioni CC.

   La proprietà setTreatSpaceAsAlphaNum in TextFormat è esposta. Per impostazione predefinita, la proprietà è False. Impostare la proprietà su True in un client per risolvere il problema relativo allo spazio scuro.

* La stringa dell’agente utente Zendesk #31620 che esce dal lettore TVSDK è troncata.

   La stringa dell’agente utente non verrà più troncata dopo 128 caratteri.

   La stringa della versione di Adobe Primetime viene aggiunta all’agente utente di sistema.

* L’evento SEEK_END mancante del #30809 Zendesk impedisce all’app di passare a uno stato di riproduzione.
* Il colore &quot;Ciano&quot; di Zendesk #30415 Closed Caption è ora una tonalità più scura di blu (turchese), rispetto alle precedenti versioni di Primetime TVSDK.

   Il colore viene cambiato da Ciano scuro a Ciano.

* Gli annunci VOD di Zendesk #30727 non vengono scaricati/risolti.

   In VMAP XML se è presente un tag VAST vuoto senza un tag di chiusura esplicito (‘&lt;/vast>&#39;) e senza un carattere di nuova riga dopo di esso, l&#39;XML VMAP non viene analizzato correttamente e gli annunci potrebbero non essere riprodotti.

**Android TVSDK 2.5.1**

* Arresto anomalo specifico del dispositivo (Samsung Galaxy Tab 4); VOD DRM LBA con Auditude e click sugli annunci.
* VHL - Le chiamate heartbeat non corrette vengono inviate quando si avvia il contenuto da un offset.
* Quando si riproducono annunci VPAID, l’heartbeat VHL richiama un evento:type:annuncio di riproduzione mancante.
* Dopo aver raggiunto lo stato COMPLETE (COMPLETATO), il lettore torna allo stato PLAY (RIPRODUZIONE) con SKIP adBreakPolicy per gli annunci post-roll.
* I cookie non vengono allegati ai callback di annunci in uscita.
* I cue point degli annunci non sono visibili.
* HLS con traccia SAP EAC3 separata non si carica.
* Il lettore si blocca quando TVSDK riceve un intento Screen On dopo il ripristino del lettore multimediale.

## Problemi noti e limitazioni {#known-issues-and-limitations}

**Android TVSDK 3.11**

* Non sono state aggiunte nuove limitazioni.

### Problemi noti e limitazioni nelle versioni precedenti

**Android TVSDK 3.10**

* Non sono state aggiunte nuove limitazioni.

**Android TVSDK 3.8**

* Non sono state aggiunte nuove limitazioni.

**Android TVSDK 3.7**

* Non sono state aggiunte nuove limitazioni.

**Android TVSDK 3.6**

* Non sono state aggiunte nuove limitazioni.

**Android TVSDK 3.5**

* Non è stata aggiunta alcuna nuova limitazione.

**Android TVSDK 3.4**

* Il supporto di ID3, sottotitoli codificati e audio di associazione tardiva non è stato verificato per il flusso CMAF (CBC).
* Su alcuni dispositivi, esiste un problema di bassa riproducibilità a causa del quale la distorsione video può apparire sulla parte superiore durante la riproduzione con trucco sui flussi CMAF.

**Android TVSDK 3.3**

* I sottotitoli clcp:c608 non sono supportati per la riproduzione di flussi CMAF.

**Android TVSDK 3.2**

* TVSDK 3.2 non supporta la riproduzione di flussi CMAF Sample AES e AES128.
* I flussi CMAF HEVC non includono il supporto per la riproduzione di sottotitoli.
* Quando la ricerca viene eseguita attorno al segmento non crittografato, viene visualizzata la colorazione verde per i flussi WV crittografati.
* I flussi CMAF non supportano gli eventi ID3.
* I flussi HLS non supportano il formato di sottotitoli TTML.

**Android TVSDK 3.0**

* In questa versione, il supporto HEVC presenta le seguenti limitazioni

   * DRM non supportato
   * Supporto CC (CEA 608/708) non verificato
   * Il supporto 4K non è ancora disponibile
   * Supporto dei tag ID3 non verificato

* Per gli eventi di avanzamento degli annunci, la barra temporale potrebbe non riflettere un tempo di riproduzione degli annunci accurato al 100%. Come soluzione alternativa, è possibile utilizzare `adcompleteevent` conoscere l’interfaccia utente di completamento e aggiornamento della riproduzione dell’annuncio per vari scopi, come aggiornare la barra temporale, rimuovere l’interfaccia utente correlata all’annuncio, ecc.
* Vaste chiamate pubblicitarie restituite da VMAP non rispettano la posizione di lookahead Just-In-Time.

**Android TVSDK 2.5.6**

* Non sono supportate più interruzioni pubblicitarie VMAP contemporaneamente.

**Android TVSDK 2.5.3**

Questa versione presenta i seguenti problemi:

* La riproduzione di video dal vivo può presentare problemi di sincronizzazione audio-video su dispositivi di fascia bassa o condizioni di rete scadenti.
* Per i flussi FER, virtualTime e localTime possono differire. Anche FER con offset non funziona.
* La riproduzione potrebbe bloccarsi quando si ricercano contenuti audio di associazione tardiva.
* A intermittenza, i sottotitoli webVTT potrebbero non essere sincronizzati per i contenuti LIVE.
* A intermittenza, è possibile vedere la riproduzione rapida di alcuni fotogrammi dopo l’uscita da un’interruzione pubblicitaria.
* A volte, viene generato l’errore 303 per le interruzioni pubblicitarie con wrapper triplo, anche se vengono riprodotti gli annunci.

**Android TVSDK 2.5.2**

Questa versione presenta i seguenti problemi:

* La riproduzione di video dal vivo potrebbe presentare problemi di sincronizzazione audio-video su dispositivi di fascia bassa.
* La riproduzione potrebbe interrompersi a volte durante la ricerca fino alla fine del file multimediale VOD.
* Per i flussi FER, virtualTime e localTime possono differire. Inoltre, FER con offset non funziona.

**Android TVSDK 2.5.1**

Questa versione di TVSDK presenta i seguenti problemi:

* La riproduzione di video dal vivo può presentare problemi di sincronizzazione audio-video su dispositivi di fascia bassa.
* Per i flussi FER, virtualTime e localTime possono differire. Inoltre, FER con offset non funziona.
* In VMAP XML, se è presente un tag VAST vuoto senza un tag di chiusura esplicito (&lt;/vast>), e senza una nuova riga successiva, l&#39;XML VMAP non viene analizzato correttamente e gli annunci potrebbero non essere riprodotti.
* Post-roll VPAID non supportati.

## Risorse utili {#helpful-resources}

* [Requisiti di sistema](/help/programming/tvsdk-3x-android-prog/android-3x-introduction/android-3x-requirements.md)
* [Guida per programmatori di TVSDK 3.10 per Android](/help/programming/tvsdk-3x-android-prog/android-3x-introduction/overview-prod-audience-guide/android-3x-overview-prod-audience-guide.md)
* [Guida di riferimento di TVSDK Android Javadoc per API](https://help.adobe.com/en_US/primetime/api/psdk/javadoc3.5/index.html)
* [Documento API TVSDK Android C++](https://help.adobe.com/en_US/primetime/api/psdk/cpp_3.5/namespaces.html) - Ogni classe Java ha una classe C++ corrispondente e la documentazione C++ contiene più materiale esplicativo rispetto ai Java, quindi fai riferimento alla documentazione C++ per una comprensione più approfondita dell’API Java.
* [Guida alla migrazione da TVSDK 1.4 a 2.5 per Android (Java)](https://helpx.adobe.com/primetime/migration-guides/tvsdk-14-25-android.html)
* Per la gestione degli scenari di attivazione/disattivazione dello schermo, vedere `Application_Changes_for_Screen_On_Off.pdf` file incluso nella build.
* Consulta la documentazione completa dell’Aiuto all’indirizzo [Informazioni e supporto per Adobe Primetime](https://helpx.adobe.com/support/primetime.html) pagina.
