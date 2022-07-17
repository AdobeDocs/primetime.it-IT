---
title: Note sulla versione di TVSDK 3.15 per Android
description: Le note sulla versione TVSDK 3.15 per Android descrivono le novità o le modifiche, i problemi risolti e noti e i problemi del dispositivo in TVSDK Android 3.15
products: SG_PRIMETIME
topic-tags: release-notes
exl-id: cd2c64ef-dd42-4dc2-805f-eeb64a8a53d9
source-git-commit: 3b051c3188c81673129e12dfeb573aaf85c15c97
workflow-type: tm+mt
source-wordcount: '5516'
ht-degree: 0%

---

# Note sulla versione di TVSDK 3.15 per Android {#tvsdk-for-android-release-notes}

Le note sulla versione TVSDK 3.15 per Android descrivono le novità o le modifiche, i problemi risolti e noti e i problemi del dispositivo in TVSDK Android 3.15.

Il lettore di riferimento Android è incluso con Android TVSDK nella directory sample/della distribuzione. Il file README.md che accompagna spiega come creare il lettore di riferimento.

>[!NOTE]
>
>Per generare correttamente il lettore di riferimento, come descritto in README.md distribuito con il rilascio, assicurati di effettuare le seguenti operazioni:
>
>1. Scarica VideoHeartbeat.jar da [https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases](https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases) (Libreria VideoHeartbeat per Android v2.0.0)
>1. Estrai VideoHeartbeat.jar nella cartella libs/ .


TVSDK per Android offre numerosi miglioramenti delle prestazioni rispetto alle versioni precedenti. Offre un&#39;esperienza di visualizzazione di alta qualità e trasporta tutte le funzioni della versione 1.4, ad eccezione del supporto Multi-CDN.

Il set completo di funzioni supportate e non supportate è presentato nella [Matrice di funzioni](#feature-matrix) nelle note sulla versione.

## Android TVSDK 3.15

Questa versione risolve il problema per cui l&#39;applicazione si blocca più volte quando manca un tag creativo o quando [!UICONTROL url CDATA] è vuoto in [!UICONTROL VAST] risposta.

Per informazioni sulle correzioni di bug in questa versione e nelle versioni precedenti, consulta [problemi risolti in TVSDK per Android](#resolved-issueszd).

### Nuove funzioni e miglioramenti introdotti nelle versioni precedenti

**Android TVSDK 3.14**

Questa versione risolve il problema di arresto anomalo dell&#39;applicazione quando [!UICONTROL CDATA] il nodo è vuoto per uno qualsiasi dei [!UICONTROL ClickTracking], [!UICONTROL CustomClick] o [!UICONTROL CompanionClickTracking] elementi nella risposta VAST.

**Android TVSDK 3.13**

Il flusso DRM di Widevine blocca o mostra fotogrammi neri su interruttore ABR su dispositivi FireTV, che includono Pendant di 3a generazione e Fire TV Cube 1a e 2a generazione dispositivi.

Per risolvere il problema, imposta l’API `MediaPlayer.flushVideoDecoderOnHeaderChange(true)` per i dispositivi Fire TV specificati prima di avviare la riproduzione. Il valore predefinito è false.

**Android TVSDK 3.12**

Aggiornamento della versione gradle dell’applicazione di riferimento di Primetime alla versione 5.6.4.

Per configurare ed eseguire l&#39;app di riferimento utilizzando Android Studio segui le istruzioni contenute nel file Leggimi disponibile con lo zip TVSDK all&#39;indirizzo `TVSDK_Android_x.x.x.x/samples/PrimetimeReference/src/README.md`.

I principali problemi risolti nella versione corrente sono menzionati in [problemi risolti](#resolved-issues) sezione .

**Android TVSDK 3.11**

* **Recupero del riquadro di intestazione specifica del sistema di protezione (PSSH) consentito** - TVSDK consente il recupero della casella di intestazione specifica del sistema di protezione associata alla risorsa multimediale caricata corrente. Nuova API `getPSSH()` aggiunto a `com.adobe.mediacore.drm.DRMManager`.

Per ulteriori informazioni, consulta [DRM](../programming/tvsdk-3x-android-prog/android-3x-content-security/android-3x-drm-widevine.md).

**Android TVSDK 3.10**

La versione si è concentrata sulla risoluzione dei principali problemi dei clienti, come indicato in [problemi risolti](#resolved-issues) sezione .

**Android TVSDK 3.9**

* **Consegna sicura tramite HTTPS** - Android TVSDK 3.9 ha introdotto le funzionalità di consegna sicura tramite HTTPS per fornire contenuti in modo sicuro con scalabilità e prestazioni senza precedenti.

   Per abilitare la consegna sicura tramite HTTPS, è stata introdotta una nuova API in `NetworkConfiguration` classe.

   `public void setForceHTTPS (boolean value)`

   `public boolean getIsForceHTTPS()`

**Android TVSDK 3.8**

* **Supporto pre-roll con funzione di Ad-Break parziale** - Con questo miglioramento, TVSDK 3.8 supporta gli annunci pre-roll con funzione di Ad-Break parziale (PABI).

L&#39;annuncio pre-roll, se disponibile, viene riprodotto e il contenuto viene riprodotto dal punto live emulando l&#39;esperienza della televisione in diretta.

**Android TVSDK 3.7**

* Per il contenuto di test Widevine, una nuova API `setMediaDrmCallback` nella classe DRMManager è esposto per ignorare l&#39;implementazione predefinita dell&#39;interfaccia MediaDrmCallback.

   `public static void setMediaDrmCallback(MediaDrmCallback callback)`

* È stato corretto l’errore AppCrash per la mancata gestione `MediaPlayerEvent.ITEM_UPDATED` in livello C++ (Android a 64 bit).

**Android TVSDK 3.6**

* **Ottimizza le tue app per il requisito dei 64 bit** - Libreria nativa `(libAVEAndroid.so)` è stato aggiornato e reso disponibile in due versioni. La posizione della libreria nativa armeabi esistente (32 bit) è stata modificata da `/framework/Player to /framework/Player/armeabi` e viene introdotta una libreria arm64-v8a (64 bit) aggiuntiva in `/framework/Player/arm64-v8a.`

**Versione 3.5**

* **Solo nel tempo e nella risoluzione degli annunci** - TVSDK 3.5 rimuove il supporto degli annunci riprodotti dalla timeline.

* **Abilitazione del supporto per la riproduzione offline** - Con la riproduzione offline, gli utenti possono ora scaricare i contenuti video sui propri dispositivi e guardarli quando non sono connessi. Per informazioni dettagliate, fare riferimento a &quot;[Riproduzione offline con Android](https://helpx.adobe.com/content/dam/help/en/primetime/programming-guides/psdk_android_3.5.pdf).&quot;

**Versione 3.4**

* TVSDK ora supporta la riproduzione di flussi CMAF per flussi crittografati e normali CBC.

**Versione 3.3**

* **Modifiche API**

   * È stata aggiunta una nuova API a `NetworkConfiguration::setNumOfTimesManifestRetryBeforeError(n)*` per gestire errori e timeout di rete.
      * dove (n) è il numero di tentativi.

**Versione 3.2**

* **Risoluzione parallela degli annunci e supporto per il download manifest**

   * TVSDK 3.2 supporta la risoluzione simultanea, invece della risoluzione sequenziale per tutte le richieste di annunci e le interruzioni di annunci, ad eccezione di VMAP.

   * Tutti i manifesti dell&#39;annuncio in un&#39;interruzione pubblicitaria vengono scaricati simultaneamente.

* **Abilitazione del supporto per la risoluzione degli annunci e il timeout del download del manifesto.**

   * Gli utenti ora possono impostare il valore di timeout per la risoluzione complessiva degli annunci e i download dei manifest.  Nel caso di VMAP, il valore di timeout si applica per singole interruzioni pubblicitarie man mano che tutte le interruzioni pubblicitarie vengono risolte in sequenza.

* **Nuove API nella classe AdvertisingMetadata:**

   * `void setAdResolutionTimeout(int adResolutionTimeout)`

   * `int getAdResolutionTimeout()`

   * `void setAdManifestTimeout(int adManifestTimeout)`

   * `int getAdManifestTimeout()`

* **Rimosso sotto API dalla classe AdvertisingMetadata:**

   * `void setAdRequestTimeout(int adRequestTimeout)`

   * `int getAdRequestTimeout()`

* **Riproduzione abilitata dei flussi con codec audio AC3/EAC3**

   * `void alwaysUseAC3OnSupportedDevices(boolean val)` in `MediaPlayer` Classe

* **TVSDK supporta la riproduzione CMAF e flussi normali per CTR Widevine crittografato.**

* **È ora supportata la riproduzione di flussi HEVC 4K.**

* **Richieste di annunci parallele** - TVSDK ora precarica 20 richieste di chiamate ad in parallelo.

**Versione 3.0**

* **TVSDK 3.0 supporta flussi HEVC (High Efficiency Video Coding).**

* **Just in Time - Risoluzione degli annunci più vicini agli ad markers**
Lazy Ad Resolving ora risolve ogni interruzione pubblicitaria in modo indipendente. In precedenza, la risoluzione degli annunci era un approccio basato su due fasi: i pre-roll sono stati risolti prima dell&#39;avvio della riproduzione e tutti gli slot mid/post roll combinati dopo l&#39;avvio della riproduzione. Con questa funzione avanzata, ogni interruzione pubblicitaria viene ora risolta in un momento specifico prima del punto di cue dell’annuncio.

>[!NOTE]
>
>La risoluzione degli annunci pigri ora è stata modificata per essere disattivata per impostazione predefinita e deve essere abilitata in modo esplicito.

È stata aggiunta una nuova API a `AdvertisingMetadata::setDelayAdLoadingTolerance` per ottenere la tolleranza per il caricamento ritardato degli annunci associata a questo metadati della pubblicità.\
La ricerca è ora consentita immediatamente dopo la PREPARAZIONE, la ricerca di ulteriori interruzioni pubblicitarie darà luogo a una risoluzione immediata prima del completamento della ricerca.\
Modalità di segnalazione `SERVER_MAP` e `MANIFEST_CUES` sono supportati.

Per ulteriori informazioni, consulta [Guida per programmatori Android TVSDK 3.0](../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/c-lazy-ad-resolving/c-lazy-ad-resolving.md) sulle modifiche apportate all’API e all’evento.

* **Aggiornato `targetSdkVersion` alla versione più recente**

Aggiornato `targetSdkVersion` da 19 a 27 per un buon funzionamento.

* **Placement.Type getPlacementType() è ora un metodo sull&#39;interfaccia TimelineMarker**

   Questo metodo restituirà un tipo di posizionamento di Placement.Type.PRE_ROLL, Placement.Type.MID_ROLL o Placement.Type.POST_ROLL. Se un&#39;interruzione pubblicitaria non è risolta, il metodo getDuration() sull&#39;interfaccia TimelineMarker restituirà 0.

**Versione 2.5.6.**

* **TVSDK 2.5 supporta Android P.**

* **Abilitazione dell&#39;audio in background**

   Per abilitare la riproduzione audio quando l’app passa dal primo piano allo sfondo, l’app deve invocare `enableAudioPlaybackInBackground` API di MediaPlayer con true come argomento quando il lettore è in stato PREPARATO.

* **alwaysUseAudioOutputLatency(valore booleano) nella classe MediaPlayer**

Quando impostato, utilizza la latenza di output nel calcolo della marca temporale audio.
Parametri booleani val - True utilizza la latenza di output audio nel calcolo della marca temporale audio.

* **Ottimizzato per ottenere la migliore esperienza di riproduzione anche se la velocità della larghezza di banda scende improvvisamente**

TVSDK ora annulla il download del segmento in corso, se necessario, e passa in modo dinamico al rendering appropriato. Questo avviene passando senza soluzione di continuità tra i bitrate senza interruzioni.

**Versione 2.5.5**

* **Inserimento di interruzioni pubblicitarie parziali**

   Esperienza simile a quella televisiva di partecipare nel mezzo di un annuncio senza attivare il tracking per l&#39;annuncio parzialmente guardato.\
   Esempio: L&#39;utente si unisce al centro (a 40 secondi) di un&#39;interruzione pubblicitaria di 90 secondi costituita da tre annunci da 30 secondi. Questo è a 10 secondi dal secondo annuncio dell&#39;interruzione.

   * Il secondo annuncio viene riprodotto per la durata rimanente (20 sec) seguita dal terzo annuncio.

   * I tracciatori degli annunci per l’annuncio parziale riprodotto (secondo annuncio) non vengono attivati. I tracciatori solo per il terzo annuncio vengono attivati.

* **Caricamento sicuro degli annunci tramite HTTPS**

   Adobe Primetime fornisce un&#39;opzione per richiedere la prima chiamata al server ad primetime e al CRS su https.

* **Aggiunta di AdSystem e ID creativo alle richieste CRS**

   Ora incluso `AdSystem` e `CreativeId` come nuovi parametri nelle richieste 1401 e 1403.

* **È stata rimossa la classe API setEncodeUrlForTracking nella classe NetworkConfiguration** poiché i caratteri non sicuri in un URL devono essere codificati.

**Versione 2.5.4**

Android TVSDK v2.5.4 offre i seguenti aggiornamenti e modifiche API:

* Modifiche al valore predefinito per `WebViewDebbuging`

   `WebViewDebbuging` è impostato su `Fals`e per impostazione predefinita. Per abilitarlo, chiama `setWebContentsDebuggingEnabled(true)` nell&#39;applicazione.

* **Aggiornamento della versione OpenSSL e Curl**

   Aggiornamento di libcurl a v7.57.0 e OpenSSL a v1.0.2k.

* Accesso a livello di app per l’oggetto di risposta VAST

   È stata introdotta una nuova API `NetworkAdInfo::getVastXml()` che fornisce l&#39;accesso dell&#39;oggetto risposta VAST all&#39;applicazione.

**Versione 2.5.3**

Android TVSDK v2.5.3 offre i seguenti aggiornamenti e modifiche API.

* Invitiamo tutti i clienti TVSDK che utilizzano CRS ad aggiornare le loro app con TVSDK 2.5.3.85 o più recente su Android. Sostituirà l’implementazione esistente dell’app. Dopo l&#39;aggiornamento TVSDK, controlla le richieste CRS creative URL in uno strumento proxy (ad esempio: Charles) e conferma che il nome host e la versione nel percorso riflettano come nella struttura dell&#39;URL di esempio seguente.

   `https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784 bf3586d.m3u8`

* Agente utente di TVSDK personalizzabile: abbiamo aggiunto alcune nuove API per personalizzare gli agenti utente.

   * `setCustomUserAgent(String value)`
   * `getCustomUserAgent()`

* Condividi cookie tra l’applicazione Android e TVSDK: Android TVSDK ora supporta l’accesso ai cookie tra il livello JAVA (memorizzato in CookieStore dell’applicazione Android) e il livello TVSDK C++. Ora è possibile impostare e/o modificare i cookie nel livello C++ nativo in quanto saranno esposti al Java Cookie Store.

* Modifiche API:

   * Un nuovo evento `CookiesUpdatedEvent` è aggiunto. Viene inviato dal lettore multimediale quando il relativo cookie viene aggiornato.

   * È stata aggiunta una nuova API a `NetworkConfiguration::set/ getCustomUserAgent()` per utilizzare un agente utente personalizzato.

   * È stata aggiunta una nuova API a `NetworkConfiguration::set/ getEncodedUrlForTracking` per forzare la codifica dei caratteri non sicuri.

   * È stata aggiunta una nuova API a `NetworkConfiguration::getNetworkDownVerificationUrl()` impostare un URL per la verifica della rete in caso di failover.

   * Viene aggiunta una nuova proprietà a `TextFormat::treatSpaceAsAlphaNum` che definiscono se considerare lo spazio come alfanumerico durante la visualizzazione delle didascalie.

* Modifiche `SizeAvailableEvent`. Precedentemente, `getHeight()` e `getWidth()` metodi `SizeAvailableEvent` in 2.5.2 utilizzato per restituire l&#39;altezza del frame e la larghezza del frame, che è stata restituita dal formato multimediale. Ora restituisce l&#39;altezza di uscita e la larghezza di uscita rispettivamente restituite dal decoder.

* Modifiche al comportamento del buffering: Il comportamento di buffering viene modificato. È lasciata allo sviluppatore di app quello che desiderano fare in caso di buffer vuoto. 2.5.3 utilizza la dimensione del buffer di riproduzione in una situazione vuota del buffer.

**Versione 2.5.2**

Android TVSDK v2.5.2 offre importanti correzioni di bug e alcune modifiche API.

**Versione 2.5.1**

Le nuove importanti funzioni rilasciate in Android 2.5.1.

* **Miglioramenti delle prestazioni -** La nuova architettura TVSDK 2.5.1 offre diversi miglioramenti delle prestazioni. Sulla base delle statistiche di uno studio di benchmarking di terze parti, la nuova architettura fornisce una riduzione 5x del tempo di avvio e 3,8x in meno rispetto alla media del settore:

* **Instant on per VOD e live -** Quando si attiva l’accesso immediato, il TVSDK inizializza e carica i contenuti multimediali prima dell’avvio della riproduzione. Poiché è possibile avviare più istanze MediaPlayerItemLoader contemporaneamente in background, è possibile creare un buffer per più flussi. Quando un utente cambia il canale e il flusso è bufferizzato correttamente, la riproduzione sul nuovo canale viene avviata immediatamente. TVSDK 2.5.1 supporta anche Instant On per **live** anche i ruscelli. I flussi live vengono ri-bufferizzati quando la finestra live si sposta.

* **Logica ABR migliorata -** La nuova logica ABR si basa sulla lunghezza del buffer, sulla velocità di variazione della lunghezza del buffer e sulla larghezza di banda misurata. In questo modo l&#39;ABR sceglie il bit rate corretto quando la larghezza di banda oscilla e ottimizza anche il numero di volte in cui l&#39;interruttore del bit rate si verifica effettivamente monitorando la velocità con cui cambia la lunghezza del buffer.

* **Download parziale del segmento/Sottosegmentazione -** TVSDK riduce ulteriormente le dimensioni di ciascun frammento, in modo da avviare la riproduzione il prima possibile. Il frammento ts deve avere un fotogramma chiave ogni due secondi.

* **Risoluzione pubblicitaria pigra -** TVSDK non attende la risoluzione degli annunci non preroll prima di avviare la riproduzione, riducendo in tal modo il tempo di avvio. Le API come ricerca e trucco non sono ancora consentite finché tutti gli annunci non vengono risolti. Questo è applicabile ai flussi VOD utilizzati con CSAI. Operazioni come ricerca e avanzamento rapido non sono consentite fino al completamento della risoluzione dell&#39;annuncio. Per i flussi live questa funzione non può essere abilitata per la risoluzione degli annunci durante un evento live.

* **Connessioni di rete persistenti -** Questa funzione consente a TVSDK di creare e memorizzare un elenco interno di connessioni di rete persistenti. Queste connessioni vengono riutilizzate per più richieste, anziché aprire una nuova connessione per ogni richiesta di rete e successivamente eliminarla. Ciò aumenta l&#39;efficienza e diminuisce la latenza nel codice di rete, consentendo prestazioni di riproduzione più veloci.
Quando TVSDK apre una connessione, richiede al server un *mantenere in vita* connessione. Alcuni server potrebbero non supportare questo tipo di connessione, nel qual caso TVSDK tornerà a stabilire una connessione per ogni richiesta. Inoltre, mentre le connessioni persistenti saranno attivate per impostazione predefinita, TVSDK dispone ora di un’opzione di configurazione che consente alle app di disattivare le connessioni persistenti, se necessario.

* **Download parallelo -** Il download di video e audio in parallelo anziché in serie riduce i ritardi di avvio. Questa funzione consente la riproduzione di file HLS Live e VOD, ottimizza l&#39;utilizzo della larghezza di banda disponibile da un server, riduce la probabilità di entrare in situazioni di sottoutilizzazione del buffer e riduce al minimo il ritardo tra il download e la riproduzione.

* **Download paralleli di annunci -** TVSDK precarica gli annunci in parallelo alla riproduzione dei contenuti prima di colpire l’annuncio, consentendo così una riproduzione fluida di annunci e contenuti.

* **Riproduzione**

* **Riproduzione di contenuti MP4 -** Le clip brevi MP4 non devono essere re-codificate per essere riprodotte in TVSDK.

   >[!NOTE]
   >
   >La commutazione ABR, la riproduzione a trucco, l&#39;inserimento di annunci, l&#39;associazione audio tardiva e la segmentazione secondaria non sono supportate per la riproduzione MP4.

* **Gioco a mattoni con bit rate adattivo (ABR) -** Questa funzione consente a TVSDK di passare da un flusso di iFrame all&#39;altro in modalità di riproduzione a trucco. È possibile utilizzare profili non iFrame per eseguire la riproduzione a velocità più basse.

* **Giocare con trucco liscio -** Questi miglioramenti migliorano l’esperienza utente:

   * Selezione del bit rate adattivo e del frame rate durante la riproduzione con trucco, in base alla larghezza di banda e al profilo del buffer

   * Utilizzare il flusso principale invece del flusso IDR per ottenere una riproduzione rapida fino a 30 fps.

* **Protezione dei contenuti**

   * **Protezione dell&#39;uscita basata sulla risoluzione** Questa funzione collega le restrizioni di riproduzione a risoluzioni specifiche, fornendo controlli DRM più precisi.

* **Supporto per i flussi di lavoro**

   * **Integrazione fatturazione diretta -** Questo invia le metriche di fatturazione al backend Adobe Analytics, certificato da Adobe Primetime per i flussi utilizzati dal cliente.

   TVSDK raccoglie automaticamente le metriche, in base al contratto di vendita del cliente, per generare rapporti di utilizzo periodici richiesti a scopo di fatturazione. In ogni evento di avvio del flusso, TVSDK utilizza l’API di inserimento dati di Adobe Analytics per inviare metriche di fatturazione come il tipo di contenuto, i flag abilitati per l’inserimento di annunci e i flag abilitati per i drm, in base alla durata del flusso fatturabile, alla suite di rapporti di proprietà di Adobe Analytics Primetime. Questo non interferisce con o viene incluso nelle suite di rapporti o nelle chiamate server del cliente Adobe Analytics. Su richiesta, questo rapporto sull’utilizzo della fatturazione viene inviato periodicamente ai clienti. Questa è la prima fase della funzione di fatturazione che supporta solo la fatturazione dell’utilizzo. Può essere configurato in base al contratto di vendita utilizzando le API descritte nella documentazione. Questa funzione è attivata per impostazione predefinita. Per disattivare questa funzione, fare riferimento al campione del lettore di riferimento.

   * **Supporto di failover migliorato -** Strategie aggiuntive implementate per continuare la riproduzione ininterrotta, nonostante gli errori dei server host, dei file playlist e dei segmenti.


* **Pubblicità**

   * **Integrazione con Moat -** Supporto per la misurazione della visualizzabilità degli annunci da Moat.

   * **Banner complementari -** I banner Companion sono visualizzati accanto a un annuncio lineare e spesso continuano a essere visualizzati sulla vista dopo la fine dell&#39;annuncio. Questi banner possono essere di tipo html (uno snippet di HTML) o di tipo iframe (un URL di una pagina iframe).

* **Analytics**

   * **VHL 2.0 -** Questa è l’integrazione più recente della Video Heartbeat Library (VHL) ottimizzata per la raccolta automatica dei dati di utilizzo per Adobe Analytics. La complessità delle API è stata ridotta per facilitare l’implementazione. Scarica la libreria VHL [v2.0.0 per Android](https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases) ed estrarre il file JAR nella cartella libs.

* **SizeAvaliableEventListener**

   * `getHeight()` e `getWidth()` metodi `SizeAvailableEvent` restituisce l&#39;output rispettivamente in altezza e larghezza. Le proporzioni di visualizzazione possono essere calcolate come segue:

      ```java
      SizeAvailableEvent e;
      DAR = e.getWidth()/ e.getHeight();
      ```

      Il rapporto di formato dello storage in termini di larghezza Sar e altezza Sar può essere utilizzato anche per calcolare la larghezza del frame e l&#39;altezza del frame:

      ```java
      SAR = e.getSarWidth()/e.getSarHeight();
      frameHeight = e.getHeight();
      frameWidth = e.getWidth()/SAR;
      ```

* **Cookie**

   * Android TVSDK ora supporta l’accesso ai cookie JAVA memorizzati in CookieStore dell’applicazione Android. Viene fornita un’API di callback (onCookiesUpdated) da registrare ogni volta che un nuovo cookie fa parte di **Set-Cookie** Intestazione della risposta. Questi cookie sono disponibili come elenco di cookie HttpCookie(s) utilizzati per un URI/dominio diverso impostando questi valori cookie su quel particolare URI/dominio utilizzando CookieStore. Analogamente, i valori dei cookie in TVSDK vengono aggiornati utilizzando l&#39;API di aggiunta CookieStore.

## Matrice di funzioni {#feature-matrix}

TVSDK per Android supporta una serie di funzioni che è possibile implementare per aggiungere funzionalità alle applicazioni video.

Nelle tabelle delle funzioni seguenti, un valore &quot;Y&quot; indica che la funzione è supportata nella versione corrente.

| Funzione | Tipo di contenuto | HLS |
|---|---|---|
| Riproduzione generale (riproduzione, pausa, ricerca) | VOD + Live | Y |
| FER - Riproduzione generale (Play, Pause, Seek) | FER VOD | Y |
| Cerca quando un annuncio è in riproduzione | VOD + Live | Non supportato |
| Riproduzione HEVC | VOD + Live | Solo contenitore fMP4 |
| AC3 ed EAC3 | VOD + Live | Non supportato |
| MP3 | VOD | Non supportato |
| Riproduzione di contenuti MP4 | VOD | Y |
| Logica di commutazione del bit rate adattivo | VOD + Live | Y |
| Riproduzione solo audio | VOD + Live | Y |
| Supporto per più reti CDN | VOD + Live | Non supportato |
| Riproduzione di annunci con supporti solo audio | VOD + Live | Non supportato |
| Sottotitoli codificati - 608/708 | VOD + Live | Y |
| Sottotitoli codificati - WebVTT | VOD + Live | Y |
| Failover manifesto | VOD + Live | Y |
| Failover avanzato | VOD + Live | Y |
| Notifiche di QoS e del lettore | VOD + Live | Y |
| Supporto per le intestazioni dei cookie | VOD + Live | Y |
| Supporto per intestazioni HTTP personalizzate | VOD + Live | Y (elenco Consentiti richiesto) |
| Imposta parametri di controllo buffer | VOD + Live | Y |
| Imposta controlli del bit rate adattivo | VOD + Live | Y |
| Tag Manifest personalizzati | VOD + Live | Y |
| Binding audio in ritardo | VOD + Live | Y |
| 302 Reindirizzamento | VOD + Live | Y |
| Riproduzione con offset | VOD + Live | Y |
| Gioco A Trick | VOD + Live | Y |
| Lento movimento in Trick Play | VOD + Live | Non supportato |
| Giocare liscio (con ABR) | VOD + Live | Y |
| Analisi ID3 | VOD + Live | Y |
| Blackout degli annunci | VOD + Live | Non supportato |
| Instant On | VOD + Live | Non supportato |
| Supporto per marker discontinuità | VOD + Live | Y |
| 302 Effetto redirect | VOD + Live | Y |

| Funzione | Tipo di contenuto | HLS |
|---|---|---|
| Riproduzione generale, annunci attivati | VOD + Live | Y |
| Contenuto FER con annunci abilitati | VOD | Y |
| Comportamenti degli annunci predefiniti | VOD + Live | Y |
| VAST 2.0/3.0 | VOD + Live | Y |
| VMAP 1.0 | VOD + Live | Y |
| Annunci MP4 | VOD + Live | Y (da CRS) |
| Gioca a mattoni con annunci abilitati | VOD + Live | Y |
| Solo annuncio | VOD | Y |
| Parametri di targeting | VOD + Live | Y |
| Parametri personalizzati | VOD + Live | Y |
| Comportamenti di annunci personalizzati | VOD + Live | Y |
| Tag personalizzati degli annunci | Live | Y |
| Ad Resolver personalizzati | VOD + Live | Y |
| Ad Resolver personalizzato | VOD | Y |
| C3 | VOD + Live | Non supportato |
| Lazy Ad Resolve | VOD | Y |
| Supporto dei marker di discontinuità - SSAI | VOD + Live | Y |
| Annunci Companion, Annunci Banner e Annunci Clickable | VOD + Live | Y |
| VPAID 2.0 | VOD + Live | Y (JS) |
| Uscita annunci in anticipo | Live | Y |
| Priorità creativa basata su regole | VOD + Live | Y |
| Regole CRS | VOD + Live | Y |
| Ad Resolver JSON | VOD + Live | Non supportato |
| Integrazione Moat | VOD + Live | Y |
| Inserimento di interruzioni pubblicitarie parziali | Live | Y |

| Funzione | Tipo di contenuto | HLS |
|---|---|---|
| Crittografia AES | VOD + Live | Y |
| Crittografia AES di esempio | VOD + Live | Y |
| Flussi token | VOD + Live | Y |
| DRM | VOD + Live | Solo contenitore fMP4 |
| DRM di Primetime | VOD + Live | Y |
| Riproduzione esterna (RBOP) | VOD + Live | Solo DRM di Primetime |
| Rotazione licenza | VOD + Live | Solo DRM di Primetime |
| Rotazione tasti | VOD + Live | Solo DRM di Primetime |

| Funzione | Tipo di contenuto | HLS |
|---|---|---|
| Integrazione Adobe Analytics VHL | VOD + Live | Y |
| Fatturazione | VOD + Live | Y |

## Problemi risolti {#resolved-issues}

Se la risoluzione è associata a un problema segnalato, viene visualizzato un riferimento Zendesk, ad esempio ZD#xxxxx.

**Android TVSDK 3.15**

Questa sezione fornisce un riepilogo del problema risolto nella versione TVSDK 3.14 Android.

* ZD#46903 - L&#39;applicazione si blocca più volte quando manca un tag creativo o quando [!UICONTROL url CDATA] è vuoto in [!UICONTROL VAST] risposta.

**Android TVSDK 3.14**

* ZD#46903 - Arresto anomalo dell&#39;applicazione quando [!UICONTROL CDATA] il nodo è vuoto per uno qualsiasi dei [!UICONTROL ClickTracking], [!UICONTROL CustomClick] o [!UICONTROL CompanionClickTracking] elemento in [!UICONTROL VAST] risposta.

### Problemi risolti nelle versioni precedenti

**Android TVSDK 3.12**

* ZD#40584 - L’app Primetime Reference non viene creata con la versione più recente di gradle.

**Android TVSDK 3.11**

* ZD#41252 - Caratteri coreani in WebVTT interrotti dopo Android 7.1.

**Android TVSDK 3.10**

* ZD#40340 - L&#39;applicazione si blocca con l&#39;errore &quot;App Not Responding&quot; durante il tentativo di riproduzione dopo il blocco elencando tutti i file TS (TypeScript).

**Android TVSDK 3.8**

* Nessun nuovo problema aggiunto.

**Android TVSDK 3.7**

* Nessun nuovo problema aggiunto.

**Android TVSDK 3.6**

* Nessun nuovo problema aggiunto.

**Versione 3.5**

* ZD#37503 - Le risposte JSON per le regole CRS vengono memorizzate nella cache per evitare le richieste duplicate.

**Versione 3.4**

* ZD#37996 - È stato risolto un problema relativo al problema di riproduzione a bassa risoluzione per flussi HEVC lineari e VOD CMAF.
* ZD#37706 - È stato risolto un problema relativo ai sottotitoli illeggibili.
* ZD#37622 - È stato risolto un problema relativo a URISyntaxErrors irreversibile per annunci specifici.
* ZD#36938 - È stato risolto un problema relativo al passaggio del bitrate al bitrate medio e quindi al bitrate più alto dopo l&#39;uscita da giochi a 30 gradi.

**Versione 3.3**

* ZD#37394 - CMAF asset fast forward causa artefatti dopo i cambiamenti di velocità.
   * È stato risolto un problema che si verificava con una modifica del profilo durante la riproduzione di un trucco.
* ZD#37396 - Mancano eventi di tracciamento degli annunci per alcuni giri/min e post-roll.
   * È stato risolto un caso specifico relativo agli eventi di tracciamento degli annunci.
* ZD#37491 - Il codice di stato HTTP con metadati di errore non è presente.
   * È stato eseguito il processo di propagazione degli errori di rete più alti nello stack.
* ZD#37808 - Elenco consentiti Nuova intestazione personalizzata.
   * Supporto SSAI_TAG aggiunto come parte di questa correzione.
* ZD#37622 - Errori di sintassi URIS da specifici Ad Pods.
   * È stato risolto un problema relativo all’arresto anomalo della riproduzione in streaming quando gli annunci dell’app Android del cliente contenenti un % non codificato
* ZD#37631 - Meccanismo di esecuzione di nuovi tentativi del manifesto principale per Android TVSDK.
   * È stata aggiunta una nuova API nella configurazione di rete per la gestione di questo miglioramento. Se questa API non viene utilizzata, il manifesto non viene ritentato. Se viene utilizzato, il manifesto verrà ritentato per la gestione degli errori e dei timeout di rete.

**Versione 3.2**

* ZD#37493- I beacon di tracciamento per la riproduzione in diretta non vengono attivati a intermittenza per il primo annuncio in sequenza.
* ZD#36985- I beacon di tracciamento non vengono inviati per interruzioni pubblicitarie vuote nella risposta VMAP.
* ZD#37134 - TVSDK genera l&#39;ID errato per la risposta VMAP a intermittenza.

**Versione 3.0**

* ZD#33740 - TVSDK genera un avviso non necessario subito dopo la creazione di un oggetto MediaPlayer e la chiamata replaceCurrentResource()

   * È stata migliorata la correzione precedente chiamando il ripristino solo quando il lettore è in stato sospeso

* ZD#36442 - Ogni nuova riproduzione disconnette la sessione di debug remoto rendendo impossibile il debug.

   * Il debug non è possibile per impostazione predefinita nella visualizzazione Web, in quanto il debug non è abilitato per impostazione predefinita. Se necessario, l’app deve abilitare il debug richiamando setWebContentsDebuggingEnabled(true) sull’oggetto restituito da MediaPlayer.getCustomAdView().

* ZD#33688 - Supporto per Just In Time e risoluzione

   * Le interruzioni pubblicitarie vengono risolte a un intervallo specificato prima della posizione dell’interruzione pubblicitaria.

* ZD#36441 - La durata della finestra dal vivo continua ad aumentare oltre i 5 minuti, causando molteplici problemi.

   * È stato risolto un problema che causava l&#39;aggiunta di due volte di virtualStartTime durante il calcolo del Live Point virtuale.

**Android TVSDK 2.5.6**

* ZD #34992 - La lingua è vuota in Sottotitoli codificati.

   * È stato corretto un caso in cui TVSDK non stava analizzando #EXT-X-MEDIA:TYPE=CLOSED-CAPTIONS dal manifesto principale per ottenere i dettagli del brano della didascalia.

* ZD #35078 - Convalida Android P.

   * TVSDK 2.5.6 è stato convalidato con le build beta Android P più recenti. Nessun problema trovato a causa del nuovo sistema operativo Android.

* ZD #34149 - Il lettore continua a richiedere manifesti anche se si verifica un errore.

   * È stato corretto il caso in cui TVSDK effettuava chiamate ripetitive anche quando tutti i profili erano inattivi (errore 404).

* ZD #31533 - Riproduzione di audio su Android dopo l&#39;invio in background dell&#39;app.

   * Aggiunto `enableAudioPlaybackInBackground` API di MediaPlayer che deve essere chiamata con &#39;True&#39; come argomento (quando il lettore è in stato PREPARATO) per abilitare la riproduzione dell&#39;audio quando l&#39;app è in background.

**Android TVSDK 2.5.5**

* ZD #21647 - Android TVSDK notifica 640x368 quando la dimensione effettiva del video è 640x360.

   * A causa della variabile m_nOutputHeight (all&#39;interno di AndroidMCVideoDecoder) che viene aggiornata con l&#39;altezza del fotogramma invece dell&#39;altezza effettiva dell&#39;output. Sono state apportate modifiche rilevanti nella funzione getVideoFrame per calcolare correttamente m_nOutputHeight.

* ZD #26614 - Urgente — Servizio di annunci di terze parti/programmatico — Mancata distribuzione delle impression.

   * È stata migliorata la correzione precedente gestendo il caso in analisi XML dove il problema era riproducibile quando &quot;space&quot; è prima del segno &quot;equal&quot; come &lt;vast version=&quot;2.0&quot;>

* ZD #29296 - Android: Aggiungi AdSystem e Creative ID alle richieste CRS.

   * Ora includendo &quot;AdSystem&quot; e &quot;CreativeId&quot; come nuovi parametri nelle richieste 1401 e 1403.

* ZD #33062 - TVSDK si blocca all&#39;occorrenza del carattere di barra nella risposta VAST sotto il nodo CDATA

   * API setEncodeUrlForTracking nella classe NetworkConfiguration rimossa come caratteri non sicuri in un URL da codificare

* ZD #33063 - La logica di selezione dei file CRS è stata interrotta - TVSDK non inviava la richiesta CRS per il formato Web ma la inviava invece per i file 3gpp.

   * È stata corretta la logica. Quando si utilizzano file multimediali con formato webm e 3gpp, CRS richiede di essere inviato per webm. E utilizzando entrambi i file multimediali con formato 3gpp, la richiesta CRS da inviare per il file con bitrate più alto 3gpp.

* ZD #33125 - L&#39;app Android si blocca con un tag DoubleClick specifico all&#39;interno del VMAP.

   * È stato corretto lo scenario per evitare l’arresto anomalo.

* ZD #32256 - Problema di rotazione della licenza e della chiave - Accesso Adobe

   * È stata corretta l’inizializzazione dei segmenti con i metadati DRM per il contenuto SampleAES. Funziona bene con i contenuti AES128.

* ZD #33619 - Avanzamento rapido di un contenuto crescente di playlist bloccato nello stato di buffering vicino al punto live.

   * Gestito il caso quando si passa al punto in diretta in modalità di gioco a trucco

* ZD #34151 - Oggetti TimedMetadata fuori servizio.

   * Due eventi TimedMetadata venivano visualizzati in ordine casuale se appartenevano alla stessa ora nella timeline. Mantenuto il loro ordine originale in manifesto.

* ZD #34189 - Problema quando si cerca l&#39;inizio della pausa pubblicitaria.

   * Il problema era con gli annunci SSAI che sono cuciti usando discontinuità. E la causa era un comportamento quando cerchiamo all&#39;inizio di tali annunci, cerchiamo un fotogramma chiave e non lo troviamo. La ragione era che la marca temporale audio minima dell’annuncio era precedente alla marca temporale del video principale. Quindi, finiamo per cercare un fotogramma chiave con dati frammentoDump errati. È stato corretto.

* ZD #34528 - La risoluzione video non viene aggiornata oltre 640x360 su FireTV 3rd gen dongle.

   * È stata migliorata la correzione per includere gli ultimi aggiornamenti del firmware

* ZD #34793 - TVSDK 2.5.x si bloccava con il risolutore di contenuti personalizzato in alcuni casi in cui VideoEngine presupponeva che le auditudeSettings fossero disponibili e non lo erano.

   * L&#39;arresto anomalo si verificava a causa di una chiamata della funzione su un puntatore condiviso Null (auditudeSettings). È stato aggiunto un controllo condizionale all’interno di VideoEngineTimeline::placeToSourceTimeline() per assicurarsi che le impostazioni di auditude siano disponibili prima di richiamare qualsiasi elemento su tale oggetto.

* ZD #32584 - Impossibile accedere alle informazioni complete presenti nel &lt;extensions> nodo di una risposta VAST.

   * È stato risolto il problema relativo all&#39;analisi XML e ora NetworkAdInfo fornisce le informazioni complete presenti nel &lt;extensions> nodo

* ZD #35086 - Mancata ricezione dei dati di estensione completi dal lettore in caso di risposte VMAP specifiche.

   * Il problema era specifico per l&#39;estensione xml in quanto l&#39;analisi XML non funzionava se l&#39;estensione xml conteneva virgolette doppie all&#39;interno del valore dell&#39;attributo. È stato risolto il problema.

**Android TVSDK 2.5.4**

* ZenDesk#33659 - Sessione di riproduzione che abilita il debug remoto della visualizzazione Web.

WebViewDebbuging è impostato su False per impostazione predefinita. Per abilitare il debug, impostare come true tramite l&#39;applicazione, utilizzando setWebContentsDebuggingEnabled(true).

* ZenDesk#33011 - La timeline dell’annuncio non è risolta in caso di richiesta CRS non riuscita.

   Quando una richiesta CRS a un annuncio non riesce, la timeline viene risolta e vengono riprodotti gli annunci rimanenti.

* ZenDesk#34528 - La risoluzione video non viene aggiornata oltre 640x360 sul dongle di terza generazione FireTV.

   La risoluzione video si attiva quando si commuta il bit rate.

* ZenDesk#33192 - AudioTrack ha un nome null quando il brano viene recuperato tramite AudioUpdatedEventListener::onAudioUpdate.

   In alcuni scenari su FireTV Stick, l&#39;evento onAudioUpdate veniva attivato quando non era presente alcun aggiornamento audio effettivo. Questo problema è stato risolto.

**Android TVSDK 2.5.3**

* La sottoscrizione tag personalizzata Zendesk#32216 - TimedMetadata non funziona.

   Stiamo restituendo i dati ID3 come array di byte (per supportare dati APIC o generici) al client, mentre nella stringa di restituzione 1.4. La matrice byte non gestisce il carattere con terminazione null, pertanto mostrava al client un carattere speciale. Questo problema è stato risolto ora.
* Zendesk#32670 - Il giocatore non arriva alla playlist ridondante

   Questo funziona correttamente ora e setNetworkDownVerificationUrl funziona come previsto.
* Zendesk#32369 - La didascalia a colori mostra oggetti o oggetti di colore diverso.

   Il problema con i problemi CC è stato risolto nella build più recente
* Zendesk#25590 - Miglioramento: Archivio cookie TVSDK ( da C++ a JAVA )

   Android TVSDK ora supporta l’accesso ai cookie tra il livello JAVA (memorizzato in CookieStore dell’applicazione Android) e il livello TVSDK C++.
* Zendesk#32252 - TVSDK_Android_2.5.2.12 non sembra avere la correzione per PTPLAY-20269

   Questo problema è stato risolto e integrato nel ramo 2.5.2.
* Zendesk#31806 - Adesivi in preparazione

   Il lettore è rimasto bloccato nello stato di preparazione perché il file xml della risposta aveva un tag vuoto. Ora il problema è risolto.
* Zendesk#31727 - I caratteri dei sottotitoli TVSDK 2.5 vengono eliminati o digitati in modo errato.

   Il problema è risolto e non viene rilasciato/visualizzato alcun carattere.
* Zendesk#31485 - DrmManager in 2.5

   Si è verificato un problema nella creazione di DrmManager tramite nuovo DrmManager(contesto contestuale). Implementata la classe DRMService che fornisce DRMManager.
* Streaming di risoluzione Zendesk#32794-1080P non riprodotto su Android

   abbiamo modificato i metodi SizeAvailableEvent e Precedentemente getHeight() e getWidth() di SizeAvailableEvent in 2.5, utilizzati per restituire l&#39;altezza del frame e la larghezza del frame, che sono stati restituiti dal formato multimediale. Ora restituisce rispettivamente l&#39;altezza in uscita e la larghezza in uscita restituite dal decoder.
* Il Flash Player Zendesk #19359 si blocca a causa della posizione dell&#39;attributo #EXT-X-FAXS-CM nel manifesto a livello di set.

   Il tag #EXT-X-FAXS-CM deve essere sempre visualizzato nella playlist principale prima che singoli bit rate o segmenti vengano visualizzati nella playlist.

**Android TVSDK 2.5.2**

* Zendesk#17305 Artifact in didascalie chiuse con sfondo non opaco.

   La proprietà setTreatSpaceAsAlphaNum in TextFormat è esposta. Per impostazione predefinita, la proprietà è impostata su False. Impostare la proprietà su True in un client per risolvere il problema di spazio scuro.

* Zendesk#25097 Il display CC presenta artefatti visivi con impostazioni CC.

   La proprietà setTreatSpaceAsAlphaNum in TextFormat è esposta. Per impostazione predefinita, la proprietà è impostata su False. Impostare la proprietà su True in un client per risolvere il problema di spazio scuro.

* La stringa dell&#39;agente utente Zendesk #31620 che esce dal lettore TVSDK è troncata.

   La stringa dell&#39;agente utente non verrà più troncata dopo 128 caratteri.

   La stringa di versione Adobe Primetime viene aggiunta all’agente utente del sistema.

* L&#39;evento SEEK_END mancante di Zendesk #30809 impedisce la transizione dell&#39;app a uno stato di riproduzione.
* Il colore &quot;ciano&quot; della didascalia chiusa di Zendesk #30415 è ora una tonalità più scura di blu (turchese) rispetto alle precedenti versioni TVSDK di Primetime.

   Il colore viene cambiato da DarkCyan a Cyan.

* Gli annunci Zendesk #30727 VOD non vengono scaricati/risolti.

   In VMAP XML se è presente un tag VAST vuoto senza un tag di chiusura esplicito (&quot;&lt;/vast>&quot;) e senza un carattere di nuova riga dopo di esso, il VMAP XML non viene analizzato correttamente e gli annunci potrebbero non essere riprodotti.

**Android TVSDK 2.5.1**

* crash specifico del dispositivo (Samsung Galaxy Tab 4); VOD DRM LBA con Auditude e clicca sugli annunci.
* VHL - Le chiamate heartbeat errate vengono inviate quando si avvia il contenuto da un offset.
* Quando vengono riprodotti gli annunci VPAID, il heartbeat VHL chiama l&#39;evento:type:Mancano gli annunci di gioco.
* Dopo aver inserito lo stato COMPLETE, il lettore torna allo stato PLAYING con SKIP adBreakPolicy per gli annunci post-roll.
* I cookie non vengono allegati ai callback degli annunci in uscita.
* I cue point degli annunci non sono visibili.
* HLS con binario SAP EAC3 separato non viene caricato.
* Il lettore si blocca quando TVSDK riceve un intento di attivazione dello schermo dopo il ripristino del Media Player.

## Problemi noti e limitazioni {#known-issues-and-limitations}

**Android TVSDK 3.11**

* Non sono state aggiunte nuove limitazioni.

### Problemi noti e limitazioni delle versioni precedenti

**Android TVSDK 3.10**

* Non sono state aggiunte nuove limitazioni.

**Android TVSDK 3.8**

* Non sono state aggiunte nuove limitazioni.

**Android TVSDK 3.7**

* Non sono state aggiunte nuove limitazioni.

**Android TVSDK 3.6**

* Non sono state aggiunte nuove limitazioni.

**Android TVSDK 3.5**

* Nessuna nuova limitazione aggiunta.

**Android TVSDK 3.4**

* ID3, sottotitoli codificati e supporto per audio a associazione ritardata non è stato verificato per il flusso CMAF (CBC).
* Su alcuni dispositivi, esiste un basso problema di riproducibilità a causa del quale la distorsione video può apparire nella parte superiore durante la riproduzione di trucco su flussi CMAF.

**Android TVSDK 3.3**

* i sottotitoli clcp:c608 non sono supportati per la riproduzione del flusso CMAF.

**Android TVSDK 3.2**

* TVSDK 3.2 non supporta la riproduzione di flussi CMAF Sample AES e AES128.
* I flussi HEVC CMAF non includono il supporto per la riproduzione di sottotitoli codificati.
* Viene visualizzata una colorazione verde per i flussi crittografati WV quando la ricerca viene eseguita intorno al segmento non crittografato.
* I flussi CMAF non supportano eventi ID3.
* I flussi HLS non supportano il formato dei sottotitoli TTML.

**Android TVSDK 3.0**

* Il supporto HEVC presenta le seguenti limitazioni in questa versione

   * DRM non supportato
   * Supporto CC (CEA 608/708) non verificato
   * Il supporto 4K non è ancora presente
   * Supporto dei tag ID3 non verificato

* Per gli eventi di avanzamento degli annunci, la barra della timeline potrebbe non riflettere il tempo di riproduzione degli annunci con precisione del 100%. Come soluzione alternativa, è possibile utilizzare `adcompleteevent` per conoscere il completamento della riproduzione degli annunci e aggiornare l’interfaccia utente per vari scopi, come aggiornare la barra della timeline, rimuovere l’interfaccia utente relativa agli annunci, ecc.
* Le chiamate ad estese restituite da VMAP non rispettano la posizione di lookahead Just-In-Time.

**Android TVSDK 2.5.6**

* Non sono supportate più interruzioni di annunci VMAP contemporaneamente.

**Android TVSDK 2.5.3**

Questa versione presenta i seguenti problemi:

* La riproduzione di video in tempo reale può presentare problemi di sincronizzazione audio-video su dispositivi di fascia bassa o condizioni di rete scadenti.
* Per i flussi FER, virtualTime e localTime possono variare. Anche la FER con offset non funziona.
* La riproduzione potrebbe bloccarsi quando i contenuti audio di associazione tardiva vengono cercati.
* A intermittenza, i sottotitoli webVTT potrebbero non essere sincronizzati per i contenuti LIVE.
* La riproduzione rapida di alcuni fotogrammi può essere vista a intermittenza dopo l&#39;uscita da un&#39;interruzione pubblicitaria.
* A volte, 303 errore viene lanciato per Tripple Wrapper Ad Breaks, anche se Ads sono giocati.

**Android TVSDK 2.5.2**

Questa versione presenta i seguenti problemi:

* La riproduzione video in diretta potrebbe presentare problemi di sincronizzazione audio-video su dispositivi di fascia bassa.
* La riproduzione può arrestarsi a volte quando si cerca la fine del supporto VOD.
* Per i flussi FER, virtualTime e localTime possono variare. Inoltre, FER con offset non funziona.

**Android TVSDK 2.5.1**

Questa versione di TVSDK presenta i seguenti problemi:

* La riproduzione di video in tempo reale può presentare problemi di sincronizzazione audio-video su dispositivi di fascia bassa.
* Per i flussi FER, virtualTime e localTime possono variare. Inoltre, FER con offset non funziona.
* In VMAP XML, se esiste un tag VAST vuoto senza un tag di chiusura esplicito (&lt;/vast>) e senza una nuova riga successiva, l&#39;XML VMAP non viene analizzato correttamente e gli annunci potrebbero non essere riprodotti.
* Il post-roll VPAID non è supportato.

## Risorse utili {#helpful-resources}

* [Requisiti di sistema](/help/programming/tvsdk-3x-android-prog/android-3x-introduction/android-3x-requirements.md)
* [Guida per programmatori Android TVSDK 3.10](/help/programming/tvsdk-3x-android-prog/android-3x-introduction/overview-prod-audience-guide/android-3x-overview-prod-audience-guide.md)
* [Guida di riferimento di riferimento per Android TVSDK per API](https://help.adobe.com/en_US/primetime/api/psdk/javadoc3.5/index.html)
* [Documento API TVSDK per Android C++](https://help.adobe.com/en_US/primetime/api/psdk/cpp_3.5/namespaces.html) - Ogni classe Java ha una classe C++ corrispondente e la documentazione C++ contiene più materiale esplicativo rispetto a Javadocs, quindi consulta la documentazione C++ per una comprensione più approfondita dell’API Java.
* [Guida alla migrazione a TVSDK da 1.4 a 2.5 per Android (Java)](https://helpx.adobe.com/primetime/migration-guides/tvsdk-14-25-android.html)
* Per gestire gli scenari di accensione/spegnimento dello schermo, vedi la `Application_Changes_for_Screen_On_Off.pdf` file incluso nella build.
* Consulta la documentazione completa dell’Aiuto all’indirizzo [Informazioni e supporto per Adobe Primetime](https://helpx.adobe.com/support/primetime.html) pagina.
