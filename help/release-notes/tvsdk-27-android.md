---
title: Note sulla versione di TVSDK 2.7 per Android™
description: Le note sulla versione di TVSDK 2.7 per Android™ descrivono le novità o le modifiche, i problemi risolti e noti e i problemi del dispositivo in TVSDK Android™ 2.7
products: SG_PRIMETIME
topic-tags: release-notes
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '4037'
ht-degree: 0%

---

# Note sulla versione di TVSDK 2.7 per Android™ {#tvsdk-for-android-release-notes}

Le note sulla versione di TVSDK 2.7 per Android™ descrivono le novità o le modifiche, i problemi risolti e noti e i problemi del dispositivo in TVSDK Android™ 2.7

## TVSDK Android™ 2.7 {#tvsdk-android}

Il lettore di riferimento Android™ è incluso con Android™ TVSDK nella directory samples/ della distribuzione. Il file README&lt;.md associato spiega come creare il lettore di riferimento.

>[!NOTE]
>
>Per creare correttamente il lettore di riferimento, come descritto nel file README.md distribuito con la versione, assicurati di effettuare le seguenti operazioni:
>
>1. Scarica VideoHeartbeat.jar da [https://github.com/Adobe-Marketing-Cloud/media-sdks/releases](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases) (Libreria VideoHeartbeat per Android™ v2.0.0)
>1. Estrai VideoHeartbeat.jar nella cartella libs/.
>

## Nuove funzioni {#new-features}

TVSDK 2.7 per Android™ include tutte le funzioni della versione 1.4 eccetto quelle non supportate elencate in [Matrice di funzioni](#feature-matrix).

**Android™ TVSDK 2.7**

* **Supporto della risoluzione degli annunci paralleli**

TVSDK 2.7 supporta la risoluzione simultanea di tutte le richieste di annunci in un’interruzione pubblicitaria, invece della risoluzione sequenziale.

### Nuove funzioni nelle versioni precedenti {#new-features-previous-releases}

**Versione 2.5.6**

* **TVSDK 2.5 supporta Android™ P**
* **Abilitazione dell&#39;audio in background**

  Per abilitare la riproduzione audio quando l’app si sposta dal primo piano in background, l’app deve chiamare enableAudioPlaybackInBackground API of MediaPlayer con true come argomento quando il lettore è in stato READY.

* **alwaysUseAudioOutputLatency(valore booleano) nella classe MediaPlayer**

Se questa opzione è impostata, utilizzate la latenza di output nel calcolo della marca temporale audio.
Valore dei parametri booleani: True utilizza la latenza di output audio nel calcolo della marca temporale audio.

* **Ottimizzato per ottenere la migliore esperienza di riproduzione anche se la velocità della larghezza di banda diminuisce improvvisamente.**
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

   * Ora inclusi `AdSystem` e `CreativeId` come nuovi parametri nelle richieste 1401 e 1403.

* **SetEncodeUrlForTracking API nella classe NetworkConfiguration rimossa** come i caratteri non sicuri in un URL devono essere codificati.

**Versione 2.5.4**

Android™ TVSDK v2.5.4 offre i seguenti aggiornamenti e modifiche API:

* Modifiche nel valore predefinito per `WebViewDebbuging`

  Il `WebViewDebbuging` valore impostato su _Falso_ per impostazione predefinita. Per abilitarlo, chiama `setWebContentsDebuggingEnabled` a _Vero_ nell&#39;applicazione.

* Aggiornamento della versione OpenSSL e Curl aggiornato `libcurl` a v7.57.0 e da OpenSSL a v1.0.2k.
* Accesso a livello di app per l’oggetto di risposta VAST È stata introdotta una nuova API NetworkAdInfo::getVastXml() che fornisce l’accesso all’applicazione dell’oggetto di risposta VAST.

**Versione 2.5.3**

Android™ TVSDK v2.5.3 offre i seguenti aggiornamenti e modifiche API.

* Tutti i clienti TVSDK che utilizzano CRS sono invitati ad aggiornare le loro app con TVSDK 2.5.3.85 o versione più recente su Android™. Si tratta di una sostituzione a cascata dell’implementazione dell’app esistente. Dopo l’aggiornamento di TVSDK, controlla le richieste dell’URL creativo di CRS in uno strumento proxy (ad esempio, Charles) e conferma che il nome host e la versione nel percorso riflettano come nella struttura dell’URL di esempio riportata di seguito.

  `https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784 bf3586d.m3u8`

* Agente utente di TVSDK personalizzabile: sono state aggiunte alcune nuove API per personalizzare gli agenti utente.

   * `setCustomUserAgent`(Valore stringa)
   * `getCustomUserAgent`()

* Condivisione di cookie tra applicazioni Android™ e TVSDK: Android™ TVSDK ora supporta l’accesso di cookie tra il livello Java™ (memorizzato in CookieStore dell’applicazione Android™) e il livello C++ TVSDK. Ora è possibile impostare e/o modificare i cookie nel livello C++ nativo quando vengono esposti al Cookie Store Java™.
* Modifiche API:

   * Viene aggiunto un nuovo Event CookiesUpdatedEvent. Viene inviato dal lettore multimediale quando il relativo cookie viene aggiornato.
   * Viene aggiunta una nuova API a `NetworkConfiguration::set/ getCustomUserAgent()` per utilizzare l’agente utente personalizzato.
   * Viene aggiunta una nuova API a `NetworkConfiguration::set/ getEncodedUrlForTracking` per forzare la codifica dei caratteri non sicuri.
   * Viene aggiunta una nuova API a `NetworkConfiguration::getNetworkDownVerificationUrl()` per impostare un URL di verifica della rete in caso di failover.
   * Viene aggiunta una nuova proprietà a TextFormat::treatSpaceAsAlphaNum che definisce se trattare lo spazio come alfanumerico durante la visualizzazione dei sottotitoli.

* Modifiche in `SizeAvailableEvent`: in precedenza, i metodi getHeight() e getWidth() di `SizeAvailableEvent` nella versione 2.5.2 veniva utilizzata per restituire l’altezza e la larghezza del frame restituite dal formato multimediale. Ora restituisce rispettivamente l&#39;altezza e la larghezza di output restituite dal decodificatore.
* Modifiche nel comportamento di buffering: il comportamento di buffering è cambiato. Spetta allo sviluppatore dell’app decidere cosa deve fare se è presente un buffer vuoto. 2.5.3 utilizza le dimensioni del buffer di riproduzione in una situazione di buffer vuoto.

**Versione 2.5.2**

Android™ TVSDK v2.5.2 offre importanti correzioni di bug e alcune modifiche API.

**Versione 2.5.1**

Le nuove importanti funzioni rilasciate in Android™ 2.5.1.

* **Miglioramenti delle prestazioni** La nuova architettura TVSDK 2.5.1 offre diversi miglioramenti delle prestazioni. In base alle statistiche di uno studio di benchmark di terze parti, la nuova architettura offre una riduzione del tempo di avvio di 5 volte e un numero di fotogrammi saltati di 3,8 volte inferiore rispetto alla media del settore:

   * **Attivazione immediata per VOD e live -** Quando attivate l&#39;opzione di attivazione immediata, TVSDK inizializza e memorizza in buffer i contenuti multimediali prima dell&#39;avvio della riproduzione. Poiché è possibile avviare più istanze MediaPlayerItemLoader contemporaneamente in background, è possibile eseguire il buffer di più flussi. Quando un utente cambia il canale e il flusso viene memorizzato correttamente nel buffer, la riproduzione sul nuovo canale inizia immediatamente. TVSDK 2.5.1 supporta anche l&#39;opzione di attivazione immediata per **live** flussi anche. I flussi in tempo reale vengono memorizzati nel buffer quando la finestra in tempo reale si sposta.

      * **Logica ABR migliorata -** La nuova logica ABR si basa sulla lunghezza del buffer, sul tasso di variazione della lunghezza del buffer e sulla larghezza di banda misurata. Questo assicura che l&#39;ABR scelga il bit rate corretto quando la larghezza di banda fluttua e ottimizza anche il numero di volte che l&#39;interruttore di bitrate si verifica effettivamente monitorando la velocità con cui cambia la lunghezza del buffer.
      * **Download/Sottosegmentazione segmento parziale -** TVSDK riduce ulteriormente le dimensioni di ciascun frammento per iniziare la riproduzione il prima possibile. Il frammento ts deve avere un fotogramma chiave ogni due secondi.
      * **Risoluzione annuncio lazy -** TVSDK non attende la risoluzione degli annunci non preroll prima di avviare la riproduzione, riducendo in tal modo il tempo di avvio. API come seek e trick-play non sono ancora consentite fino a quando tutti gli annunci non sono risolti. Questo è applicabile ai flussi VOD utilizzati con CSAI. Operazioni come ricerca e avanzamento rapido non sono consentite fino al completamento della risoluzione dell’annuncio. Per i flussi live, questa funzione non può essere abilitata per la risoluzione degli annunci durante un evento live.
      * **Connessioni di rete persistenti -** Questa funzione consente a TVSDK di creare e memorizzare un elenco interno di connessioni di rete persistenti. Queste connessioni vengono riutilizzate per più richieste, anziché aprire una nuova connessione per ogni richiesta di rete e quindi eliminarla in seguito. Ciò aumenta l’efficienza e diminuisce la latenza nel codice di rete, con conseguente miglioramento delle prestazioni di riproduzione.
Quando TVSDK apre una connessione, richiede al server di *keep-alive* connessione. Alcuni server potrebbero non supportare questo tipo di connessione, nel qual caso TVSDK tornerà a effettuare una connessione per ogni richiesta. Inoltre, mentre le connessioni persistenti sono attive per impostazione predefinita, TVSDK ora dispone di un&#39;opzione di configurazione che consente alle app di disattivare le connessioni persistenti, se necessario.
      * **Download parallelo -** Il download di video e audio in parallelo anziché in serie riduce i ritardi di avvio. Questa funzione consente la riproduzione di file HLS Live e VOD, ottimizza l&#39;utilizzo della larghezza di banda disponibile da un server, riduce la probabilità di entrare in situazioni di buffer underrun e riduce al minimo il ritardo tra il download e la riproduzione.
      * **Download paralleli di annunci -** TVSDK preacquisisce gli annunci in parallelo alla riproduzione del contenuto prima che l’annuncio venga interrotto, consentendo in tal modo una riproduzione fluida di annunci e contenuti.

* **Riproduzione**

   * **Riproduzione di contenuti MP4 -** Non è necessario ripetere la trascodifica di clip MP4 brevi per la riproduzione in TVSDK.
Nota: la commutazione ABR, la riproduzione mediante trick, l&#39;inserimento di annunci, l&#39;associazione audio in ritardo e la sottosegmentazione non sono supportate per la riproduzione MP4.
   * **Riproduzione &quot;trrick&quot; con velocità bit adattiva (ABR) -** Questa funzione consente a TVSDK di passare da un flusso iFrame a un altro in modalità &quot;trick play&quot;. È possibile utilizzare profili non iFrame per eseguire la riproduzione a velocità inferiori.
   * **Gioco più fluido -** Questi miglioramenti migliorano l’esperienza utente:

         * Selezione del bit rate e del frame rate adattivo durante la riproduzione con &quot;trick&quot;, in base alla larghezza di banda e al profilo del buffer
         * Utilizzo dello streaming principale invece dello streaming IDR per ottenere una riproduzione rapida fino a 30 fps.
     
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

   * **VHL 2.0 -** Questa è la più recente integrazione ottimizzata della Video Heartbeat Library (VHL) per la raccolta automatica dei dati di utilizzo per Adobe Analytics. La complessità delle API è stata ridotta a per semplificare l’implementazione. Scarica la libreria VHL [v2.0.0 per Android™](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases) ed estrarre il file JAR nella cartella libs.

* **SizeAvaliableEventListener**
   * I metodi getHeight() e getWidth() di SizeAvailableEvent restituiranno ora l&#39;output rispettivamente in altezza e larghezza. Le proporzioni di visualizzazione possono essere calcolate come segue:

     ```
     SizeAvailableEvent e;
     
     DAR = e.getWidth()/ e.getHeight();
     
     Storage Aspect Ratio in terms of Sar width and Sar height can also be used to calculate Frame width and Frame height:
     
     SAR = e.getSarWidth()/e.getSarHeight();
     
     frameHeight = e.getHeight();
     
     frameWidth = e.getWidth()/SAR;    
     ```

* **Cookie**

   * Android™ TVSDK ora supporta l’accesso ai cookie Java™ memorizzati in CookieStore dell’applicazione Android™. Viene fornita un’API di callback (onCookiesUpdated) per registrare ogni volta che un nuovo cookie arriva come parte dell’intestazione di risposta &quot;Set-Cookie&quot;. Questi cookie sono disponibili come elenco di cookie HTTP utilizzati per un URI/dominio diverso impostando questi valori cookie su quel particolare URI/dominio utilizzando CookieStore. Allo stesso modo, i valori dei cookie in TVSDK vengono aggiornati utilizzando l’API di aggiunta CookieStore.

## Matrice di funzioni {#feature-matrix}

TVSDK per Android™ supporta varie funzioni che è possibile implementare per aggiungere funzionalità alle applicazioni video.

Nelle tabelle delle funzioni riportate di seguito, una &quot;Y&quot; indica che la funzione è supportata nella versione corrente.

| Funzionalità | Tipo di contenuto | HLS |
|---|---|---|
| Riproduzione generale (riproduzione, pausa, ricerca) | VOD + Live | Y |
| FER - Riproduzione generale (riproduzione, pausa, ricerca) | VOD FER | Y |
| Ricerca durante la riproduzione di un annuncio | VOD + Live | Non supportato |
| AC3 | VOD + Live | Non supportato |
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
| Riproduzione solo audio | VOD + Live | Y |
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

| Funzionalità | Tipo di contenuto | HLS |
|---|---|---|
| Crittografia AES | VOD + Live | Y |
| Esempio di crittografia AES | VOD + Live | Y |
| Flussi con token | VOD + Live | Y |
| DRM | VOD + Live | Solo DRM di Primetime (in futuro: Widevine) |
| Riproduzione esterna (RBOP) | VOD + Live | Solo DRM di Primetime |
| Rotazione licenza | VOD + Live | Solo DRM di Primetime |
| Rotazione tasti | VOD + Live | Solo DRM di Primetime |

| Funzionalità | Tipo di contenuto | HLS |
|---|---|---|
| Integrazione Adobe Analytics VHL | VOD + Live | Y |
| Fatturazione | VOD + Live | Y |

## Problemi risolti {#resolved-issues}

Se la risoluzione è associata a un problema segnalato, viene visualizzato un riferimento Zendesk, ad esempio ZD#xxxxx

**Android™ TVSDK 2.7**

Questa sezione fornisce un riepilogo del problema risolto nella versione di TVSDK 2.7.

* ZD#37166 - La chiamata di tracciamento degli errori viene attivata anche quando l’annuncio viene riprodotto correttamente.
* ZD#37134 - Vengono restituiti ID annuncio errati, nel caso in cui l’annuncio wrapper(3P) sia presente con più annunci nella risposta VMAP.

**Android™ TVSDK 2.5.6**

* #34992 ZD - La lingua nei sottotitoli codificati è vuota.
   * È stato risolto un caso in cui TVSDK non stava analizzando #EXT-X-MEDIA:TYPE=CLOSED-CAPTIONS dal manifesto principale per ottenere i dettagli del tracciamento della didascalia.
* ZD #35078 - Convalida P per Android.
   * TVSDK 2.5.6 è stato convalidato con le build beta più recenti di Android™ P. Nessun problema trovato a causa del nuovo sistema operativo Android™.
* #34149 ZD: il lettore continua a richiedere i manifesti anche se si verifica un errore.
   * È stato risolto il caso in cui TVSDK effettuava chiamate ripetitive anche quando tutti i profili non erano attivi (errore 404).
* ZD #31533 - Riproduzione di audio su Android™ dopo l’invio in background dell’app.
   * Aggiunto `enableAudioPlaybackInBackground` API di MediaPlayer che deve essere chiamata con &quot;True&quot; come argomento (quando il lettore è in stato READY) per abilitare la riproduzione di audio quando l’app è in background.

**Android™ TVSDK 2.5.5**

* ZD #21647 - Android TVSDK notifica 640x368 quando la dimensione video effettiva è 640x360.
   * A causa della variabile m_nOutputHeight (all’interno di AndroidMCVideoDecoder) che viene aggiornata con l’altezza del fotogramma invece dell’altezza di output effettiva. Sono state apportate modifiche rilevanti alla funzione getVideoFrame per calcolare correttamente m_nOutputHeight.
* ZD #26614 - Urgente — terza parte ad serving / programmatico — incapacità di servire impressioni.
   * È stata migliorata la correzione precedente gestendo il caso nell’analisi XML in cui il problema era riproducibile quando &quot;spazio&quot; è prima del segno &quot;uguale a&quot; come &lt;vast version=&quot;2.0&quot;>
* ZD #29296 - Android: aggiungi AdSystem e Creative ID alle richieste CRS.
   * Ora inclusione di &quot;AdSystem&quot; e &quot;CreativeId&quot; come nuovi parametri nelle richieste 1401 e 1403.
* #33062 ZD - TVSDK si blocca al verificarsi del carattere di barra verticale nella risposta VAST sotto il nodo CDATA
   * API setEncodeUrlForTracking nella classe NetworkConfiguration rimossa come caratteri non sicuri in un URL da codificare.
* #33063 ZD: la logica di selezione del file CRS è stata interrotta. TVSDK non inviava richieste CRS per il formato webm, ma per i file 3gpp.
   * È stata corretta la logica. Quando si utilizzano file multimediali con formato webm e 3gpp, CRS richiede di essere inviato per webm. Quando si utilizzano entrambi i file multimediali in formato 3gpp, la richiesta CRS viene inviata per il file 3gpp con bitrate più elevato.
* ZD #33125 - L’app Android si blocca con un tag DoubleClick specifico all’interno della VMAP.
   * È stato corretto lo scenario per evitare l’arresto anomalo.
* #32256 ZD - Problema relativo alla rotazione delle licenze e alla rotazione dei tasti - Accesso agli Adobi.
   * È stata corretta l’inizializzazione dei segmenti con i metadati DRM per il contenuto SampleAES. Compatibile con contenuti AES128.
* ZD #33619 - Avanzamento rapido di una playlist in crescita bloccata nello stato di buffering vicino a un punto live.
   * Gestiva il caso durante l’attraversamento del punto live in modalità di gioco trick.
* #34151 ZD - Oggetti TimedMetadata non ordinati.
   * Due eventi TimedMetadata venivano visualizzati in ordine casuale se appartenevano alla stessa ora nella timeline. Mantenuto l&#39;ordine originale nel manifesto.
* ZD #34189 - Problema durante la ricerca dell’inizio dell’interruzione pubblicitaria.
   * Il problema era con gli annunci SSAI che vengono uniti utilizzando la discontinuità. E la causa era un comportamento quando cerchiamo l&#39;inizio di queste pubblicità, cerchiamo un fotogramma chiave e non lo troviamo. Il motivo era che il timestamp audio minimo dell’annuncio era precedente al timestamp video minimo. Pertanto, finiamo per cercare un fotogramma chiave in un frammentoDati dump errato. Corretto ora.
* ZD #34528 - Risoluzione video non aggiornamento oltre 640x360 su FireTV 3a gen dongle.
   * Miglioramento della correzione per includere gli aggiornamenti del firmware più recenti.
* ZD #34793 - TVSDK 2.5.x utilizzava l’arresto anomalo con il risolutore dei contenuti personalizzato talvolta quando VideoEngine supponeva che le impostazioni di controllo dell’audience fossero disponibili e non lo fossero.
   * L’arresto anomalo era dovuto a una chiamata di funzione su un puntatore condiviso Null (auditudeSettings). È stato aggiunto un controllo condizionale in VideoEngineTimeline::placeToSourceTimeline() per verificare che auditudeSettings sia disponibile prima di richiamare qualsiasi elemento su tale oggetto.
* #32584 ZD - Impossibile accedere alle informazioni complete presenti nel &lt;extensions> nodo di una risposta VAST.
   * È stato risolto il problema relativo all&#39;analisi XML e ora NetworkAdInfo fornisce le informazioni complete presenti nel &lt;extensions> nodo.
* ZD #35086 - Non si ottengono dati completi sull’estensione dal lettore in presenza di risposte VMAP specifiche.
   * Il problema era specifico dell’estensione xml poiché l’analisi XML non funzionava se l’estensione xml conteneva virgolette doppie all’interno del valore dell’attributo. È stato risolto il problema.

**Android™ TVSDK 2.5.4**

* ZenDesk#33659 - Sessione di riproduzione che abilita il debug remoto di webview.
   * WebViewDebbuging è impostato su False per impostazione predefinita. Per abilitare il debug, impostare come true tramite l&#39;applicazione utilizzando setWebContentsDebuggingEnabled(true).
* ZenDesk#33011 - La timeline dell’annuncio non viene risolta in caso di richiesta CRS non riuscita.
   * Quando una richiesta CRS a un annuncio non riesce, la timeline viene risolta e gli annunci rimanenti vengono riprodotti.
* ZenDesk#34528 - La risoluzione video non si aggiorna oltre 640x360 su dongle FireTV di terza generazione.
   * La risoluzione video si attiva come commutatori della velocità di trasmissione.
* ZenDesk#33192 - AudioTrack ha un nome null quando il brano viene recuperato tramite AudioUpdatedEventListener::onAudioUpdated.
   * In alcuni scenari su FireTV Stick, l&#39;evento onAudioUpdate veniva attivato quando non vi era alcun aggiornamento audio effettivo. Questo problema è stato risolto adesso.

**Android™ TVSDK 2.5.3**

* Zendesk#32216 - L’abbonamento tag personalizzato TimedMetadata non funziona.
   * Stiamo restituendo i dati ID3 come una matrice di byte (per supportare dati APIC o generici) al client, mentre nella stringa restituita 1.4. L’array di byte non gestisce il carattere null terminated in sé, pertanto mostrava al client un carattere speciale. Questo problema è stato risolto adesso.
* Zendesk#32670 - Impossibile eseguire il failover del lettore sulla sequenza di riproduzione ridondante
   * Questa operazione ora funziona correttamente e setNetworkDownVerificationUrl funziona come previsto.
* Zendesk#32369 - La didascalia mostra diversi colori di rifiuti o artefatti.
   * Il problema relativo ai glitch CC è stato risolto nella build più recente
* Zendesk#25590 - Miglioramento: archivio cookie TVSDK (da C++ a Java™)
   * Android™ TVSDK ora supporta l’accesso ai cookie tra il livello Java™ (memorizzato in CookieStore dell’applicazione Android™) e il livello C++ TVSDK.
* Zendesk#32252 - TVSDK_Android_2.5.2.12 non sembra avere la correzione per PTPLAY-20269 Questo problema è stato risolto e integrato nel ramo 2.5.2.
* Zendesk#31806 - I bastoni di Auditude in PREPARAZIONE del lettore sono bloccati in stato di preparazione perché l&#39;XML di risposta aveva un tag vuoto. Ora il problema è risolto.
* Zendesk#31727 - I caratteri di sottotitoli codificati TVSDK 2.5 non vengono inseriti o contengono un errore di ortografia.
   * Il problema è risolto e non verrà eliminato o digitato in modo errato alcun carattere.
* Zendesk#31485 - DrmManager in 2.5
   * Si è verificato un problema nella creazione di DrmManager tramite il nuovo DrmManager (contesto di contesto). È stata implementata la classe DRMService che fornirebbe DRMManager.
* Zendesk#32794- Il flusso di risoluzione 1080P non viene riprodotto su Android™.
   * È stato modificato SizeAvailableEvent. Precedentemente, `getHeight()` e `getWidth()` metodi di SizeAvailableEvent in 2.5 utilizzati per restituire l&#39;altezza e la larghezza del frame, restituite dal formato multimediale. Ora restituisce rispettivamente l&#39;altezza e la larghezza di output restituite dal decodificatore.
* Il Flash Player di #19359 Zendesk si blocca a causa della posizione di #EXT-X-FAXS-CM attributo nel manifesto a livello di set.
   * Il tag #EXT-X-FAXS-CM deve sempre comparire nella playlist principale prima che singoli bitrate o segmenti vengano visualizzati nella playlist.

**Android™ TVSDK 2.5.2**

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

**Android™ TVSDK 2.5.1**

* Arresto anomalo specifico del dispositivo (Samsung Galaxy Tab 4); VOD DRM LBA con Auditude e clic sugli annunci.
* VHL - Le chiamate heartbeat non corrette vengono inviate quando si avvia il contenuto da un offset.
* Quando si riproducono annunci VPAID, l’heartbeat VHL richiama un evento:type:annuncio di riproduzione mancante.
* Dopo aver raggiunto lo stato COMPLETE (COMPLETATO), il lettore torna allo stato PLAY (RIPRODUZIONE) con SKIP adBreakPolicy per gli annunci post-roll.
* I cookie non vengono allegati ai callback di annunci in uscita.
* I cue point degli annunci non sono visibili.
* HLS con traccia SAP EAC3 separata non si carica.
* Il lettore si blocca quando TVSDK riceve un intento Screen On dopo il ripristino del lettore multimediale.

## Problemi noti e limitazioni {#known-issues-and-limitations}

**Android™ TVSDK 2.7**

* TVSDK 2.7 supporta la risoluzione simultanea di un massimo di cinque annunci.
* Nel caso di una risposta VMAP, le chiamate dell’annuncio in un’unica interruzione pubblicitaria vanno simultaneamente e le interruzioni pubblicitarie vengono risolte in sequenza.
* Nel caso di un FER, le chiamate di annuncio in ogni opportunità vengono risolte contemporaneamente.

### Problemi noti e limitazioni nelle versioni precedenti{#known-issues-limitations-previous-releases}

**Android™ TVSDK 2.5.6**

* Non sono supportate più interruzioni pubblicitarie VMAP contemporaneamente.

**Android™ TVSDK 2.5.3**

Questa versione presenta i seguenti problemi:

* La riproduzione di video dal vivo può presentare problemi di sincronizzazione audio-video su dispositivi di fascia bassa o condizioni di rete scadenti.
* Per i flussi FER, virtualTime e localTime possono differire. Anche FER con offset non funziona.
* La riproduzione potrebbe bloccarsi quando si ricercano contenuti audio di associazione tardiva.
* A intermittenza, i sottotitoli webVTT potrebbero non essere sincronizzati per i contenuti LIVE.
* A intermittenza, è possibile vedere la riproduzione rapida di alcuni fotogrammi dopo l’uscita da un’interruzione pubblicitaria.
* A volte, viene generato un errore 303 per Triple Wrapper Ad Breaks, anche se vengono riprodotti annunci.

**Android™ TVSDK 2.5.2**

Questa versione presenta i seguenti problemi:

* La riproduzione di video dal vivo potrebbe presentare problemi di sincronizzazione audio-video su dispositivi di fascia bassa.
* La riproduzione potrebbe interrompersi a volte durante la ricerca fino alla fine del file multimediale VOD.
* Per i flussi FER, virtualTime e localTime possono differire. Inoltre, FER con offset non funziona.

**Android™ TVSDK 2.5.1**

Questa versione di TVSDK presenta i seguenti problemi:

* La riproduzione di video dal vivo può presentare problemi di sincronizzazione audio-video su dispositivi di fascia bassa.
* Per i flussi FER, virtualTime e localTime possono differire. Inoltre, FER con offset non funziona.
* In VMAP XML, se è presente un tag VAST vuoto senza un tag di chiusura esplicito (&lt;/vast>), e senza una nuova riga successiva, l&#39;XML VMAP non viene analizzato correttamente e gli annunci potrebbero non essere riprodotti.
* Post-roll VPAID non supportati.

## Risorse utili {#helpful-resources}

* [Requisiti di sistema](/help/programming/tvsdk-2.7-for-android/c-psdk-android-2.7-requirements.md)
* [Guida per programmatori di TVSDK 2.7 per Android™](/help/programming/tvsdk-2.7-for-android/overview-prod-audience-guide/c-psdk-android-2.7-overview-prod-audience-guide.md)
* [Guida di riferimento di TVSDK per Android™ Javadoc per API](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.7/index.html)
* [Documento API TVSDK Android™ C++](https://help.adobe.com/en_US/primetime/api/psdk/cpp/namespaces.html) - Ogni classe Java™ ha una classe C++ corrispondente e la documentazione C++ contiene più materiale esplicativo rispetto ai documenti Java™, quindi fai riferimento alla documentazione C++ per una comprensione più approfondita dell’API Java™.
* [Guida alla migrazione da TVSDK 1.4 a 2.5 per Android™ (Java™)](/help/migration-guides/tvsdk-14-25-android.md)
* Per la gestione degli scenari di attivazione/disattivazione dello schermo, vedere `Application_Changes_for_Screen_On_Off.pdf` file incluso nella build.
* Consulta la documentazione completa dell’Aiuto all’indirizzo [Informazioni e supporto per Adobe Primetime](https://experienceleague.adobe.com/docs/primetime.html) pagina.
