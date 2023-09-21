---
title: Note sulla versione di TVSDK 1.4 per HLS desktop
description: Le note sulla versione di TVSDK per HLS desktop descrivono le novità o le modifiche, i problemi risolti e noti in TVSDK DHLS.
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: release-notes
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '5194'
ht-degree: 0%

---

# Note sulla versione di TVSDK 1.4 per HLS desktop {#tvsdk-for-desktop-hls-release-notes}

Le note sulla versione di TVSDK per HLS desktop descrivono le novità o le modifiche, i problemi risolti e i problemi noti in TVSDK DHLS.

## Nuove funzioni {#new-features}

**1.4.31**

* **Supporto multi-CDN per annunci CRS**

   * Per impostazione predefinita, tutte le risorse trascodificate saranno ospitate su CDN di proprietà dell’Adobe in Akamai. Con la versione più recente, Adobe Creative Repackaging Service (CRS) consente di caricare i contenuti creativi transcodificati su più CDN come specificato dal cliente.
   * Vengono aggiunte nuove API a TVSDK per abilitare la specifica dell’URL creativo CRS finale quando non viene utilizzato l’URL predefinito. Per informazioni su come utilizzare queste nuove API, consulta la documentazione.

### Nuove funzioni nelle versioni precedenti {#new-features-previous}

**1.4.30**

* **Metriche di fatturazione**

Per soddisfare i clienti che desiderano pagare solo per ciò che utilizzano, anziché una tariffa fissa indipendentemente dall’uso effettivo, Adobe raccoglie le metriche di utilizzo e le utilizza per determinare quanto fatturare ai clienti.

**1.4.24**

* **Connessione di rete persistente**

Importante: è necessario che sia installato almeno Adobe Flash Player versione 22 o successiva.
Le connessioni di rete persistenti creano e memorizzano un elenco interno di connessioni di rete che possono essere riutilizzate per più richieste, anziché aprire una nuova connessione per ogni richiesta di rete. Le connessioni di rete persistenti dovrebbero aumentare l’efficienza e ridurre la latenza nel codice di rete.

In questa versione, questa funzione non è supportata in Apple Safari e Mozilla Firefox su Mac.

**1.4.19**

* Supporto dell’integrità dello streaming per gli annunci VPAID.
* Abilitazione dell’opzione Disattiva audio nel lettore di Flash FP 20.0.0.267 per Firefox 42 e versioni successive per la risoluzione del problema di blocco.

**1.4.18**

* Primetime Desktop HLS TVSDK ora supporta i creativi di VPAID 2.0 Linear SWF per consentire un’esperienza pubblicitaria interattiva in-stream.

**1.4.10**

* **Fallback degli annunci, concatenamento a margherita nella logica di selezione degli annunci (#3103 Zendesk)** Per gli annunci VAST (creativi) con la regola di fallback abilitata, TVSDK tratta un annuncio con un tipo MIME non valido come annuncio vuoto e tenta di utilizzare gli annunci di fallback al suo posto. Puoi configurare alcuni aspetti del comportamento di fallback.

Per ulteriori informazioni, consulta [Fallback degli annunci per annunci VAST e VMAP](../programming/tvsdk-1.4-for-android/ad-insertion/ad-fallback/android-1.4-ad-fallback.md).

**1.4.8**

* **Video Heartbeats Library (VHL) aggiornato alla versione 1.5**

   * Possibilità di inviare metadati con avvio video e/o inizio video/annuncio/capitolo come dati contestuali
   * Meno traffico di rete: gli heartbeat sono in media meno numerosi e di dimensioni più ridotte.

**1.4.7**

* **Supporto per la personalizzazione on-premise**

Supporto per le installazioni on-premise di Adobe Individualization Server per personalizzare la richiesta di personalizzazione del client in modo da passare a un endpoint diverso.

**1.4.6**

* **Esempio di crittografia AES (richiede la versione di Flash Player 17.0.0.134)**

È ora supportata la crittografia AES basata su esempi.

**1.4.2**

* **Aggiornamento Video Heartbeats Library (VHL) alla versione 1.4.0.1**

   * Con Adobe Analytics Video Essentials è stata aggiunta la possibilità di unire diversi casi di utilizzo di analisi da altri SDK o lettori.
   * Il tracciamento degli annunci è stato ottimizzato rimuovendo i metodi trackAdBreakStart e trackAdBreakComplete. L’interruzione pubblicitaria viene dedotta dalle chiamate dei metodi trackAdStart e trackAdComplete.
   * La proprietà della testina di riproduzione non è più necessaria durante il tracciamento degli annunci.

**1.4.0**

* **Segnalazione Di Sospensione Attività Con Sostituzione Contenuti Alternativa** Come parte dell’aggiornamento 1.4 TVSDK, ora TVSDK supporta anche l’entrata e la restituzione da blackout regionali rispetto ai contenuti lineari. TVSDK è ora in grado di elaborare due file manifest in parallelo, principale e alternativo, per monitorare i segnali di blackout anche quando viene mostrata una programmazione alternativa al posto della programmazione originale.

* **Rimuovi/Sostituisci annunci C3** Ora non è necessario alcun lavoro di preparazione aggiuntivo per inserire dinamicamente nuovi annunci nelle risorse video on demand (VOD) che escono dalla finestra C3. TVSDK ora fornisce un’API per rimuovere intervalli di contenuti personalizzati e inserire dinamicamente nuovi annunci. Questa nuova potente funzionalità è utile anche nei casi in cui i contenuti live/lineari vengano trasmessi durante la trasmissione e vengono immediatamente abbassati per essere utilizzati come contenuti on-demand senza il tempo necessario per &quot;ripulire&quot; la risorsa.

## Problemi risolti {#resolved-issues}

>[!NOTE]
>
>Tutti i clienti TVSDK che utilizzano CRS sono vivamente invitati ad effettuare l’aggiornamento almeno a TVSDK 1.4.32 su iOS, Android e Desktop HLS. Questo aggiornamento sostituirà l’implementazione dell’app esistente. Dopo l’aggiornamento, controlla le richieste dell’URL creativo di CRS in uno strumento proxy (ad esempio, Charles) per verificare che la versione nel percorso rifletta la versione 3.1. Ad esempio:
>
>`https://adunit.cdn.auditude.com/assets/3p/v3.1/218747/94b/c1b/94bc1b964cc67e115a5a6781c7329b90_ee92607938ffff46b083121f044c2746.m3u8`

**Versione 1.4.41**

* #33777 Zendesk - Token SWF Localhost scaduto per la build di distribuzione DHLS.

  Aggiornamento del token localhost per la demo PMP su DHLS.

### Problemi risolti nelle versioni precedenti {#resolved-issues-previous}

**Versione 1.4.38** (891)

* Zendesk #30731 - TVSDK non riproduce più annunci VPAID in un AdBreak.

  È stata corretta la riproduzione di più annunci VPAID in un AdBreak.

* Zendesk #29968 - Cartellone doppio.

  Il lettore video può ripetere l&#39;ultimo segmento di un periodo quando si verifica un interruttore ABR. Per questo motivo, a volte, l’ultimo segmento di preroll si è ripetuto. Questo problema è stato risolto.

**Versione 1.4.35** (879)

* #26058 Zendesk - Supporto di eventi VPAID nativi

**Versione 1.4.33** (873)

* Zendesk #21701 - Invia l’URL creativo originale per la richiesta 1401 CRS invece dell’URL normalizzato.

  È stato risolto il problema relativo alla richiesta di transcodifica di URL già inseriti nel pacchetto, in base a quanto richiesto dal back-end CRS.
* Zendesk #26197 - Compressione anamorfica non riprodotta nella risoluzione desiderata del display.

  **Nota**: questo problema richiede Flash Player 24.0.0.194 o versione successiva.

  È stato risolto il problema per cui le voci mancanti nelle tabelle delle proporzioni venivano utilizzate per calcolare la larghezza dell’output.

* Zendesk #26840 - Rilevamento HDCP non riuscito su IE11 + Windows7 dopo il secondo tentativo.

  **Nota**: questo problema richiede il lettore Flash 24.0.0.218 o versione successiva.

  Questo problema è stato risolto modificando l’elaborazione della coda di messaggi principale di AdobeCP in modo da eseguire l’iterazione nell’intera coda, invece di bloccare solo il primo messaggio.

* Zendesk #27460 - Il nuovo account Akamai non è in grado di gestire una richiesta CDN di POST.

  Il nuovo account CDN non è in grado di gestire una richiesta CDN di POST. Questo problema è stato risolto aggiornando il codice in modo che la richiesta dell’annuncio cdn.auditude.com sia GET anziché POST.
* Zendesk #27619 - Arresto anomalo del Flash su Windows 10

  **Nota**: questo problema richiede il lettore Flash 24.0.0.218 o versione successiva.

  Questo problema è stato risolto evitando un errore dovuto alla presenza di URL lunghi.

* Zendesk #28218 - L’evento di tracciamento non si attiva durante il plackback dal punto di ripresa

  Questo problema è lo stesso di Zendesk #26592. È stato risolto il problema per cui le operazioni di ricerca erano consentite quando il lettore multimediale è in stato PREPARATO per i flussi VOD.

**Versione 1.4.32** (867)

* L’evento di tracciamento di Zendesk #26592 non si attiva quando la riproduzione inizia dal punto di ripresa

Il codice non aggiornava l’elemento di interruzione pubblicitaria pre-roll quando il punto di ripresa non era zero. Questo problema è stato risolto aggiungendo una logica per aggiornare il codice quando gli orari di inizio dell’intervallo non corrispondono.

* Zendesk #27022 Ads non viene riprodotto la seconda volta che si riproduce una risorsa

Le eccezioni con i metodi array sono state corrette.

**Versione 1.4.30** (855)

In questa versione sono stati risolti i seguenti problemi per TVSDK:

* Zendesk #22898 - I sottotitoli mancanti non dovrebbero causare errori di riproduzione.

**Nota**: questo problema richiede Flash Player 23.0.0.185 o versione successiva.

Questo problema è stato risolto consentendo a TVSDK di continuare la riproduzione, anche se nel manifesto manca WebVTT M3U8, e di registrare un avviso.

* Zendesk #23454 - Gli annunci di terze parti (VPAID) non vengono gestiti correttamente

Questo problema è stato risolto gestendo correttamente gli annunci VPAID in base agli ID contenuto anziché agli intervalli di tempo.

* Zendesk #24528 - Metriche di utilizzo TVSDK per la fatturazione.

Importante: questo problema richiede Flash Player 23.0.0.185 o versione successiva.

* Zendesk # 25432 problema di sottotitoli codificati durante il ridimensionamento del lettore.

Importante: questo problema richiede Flash Player 23.0.0.185 o versione successiva.

La didascalia del codice della mappa texture è stata corretta per gestire correttamente le coordinate durante il ridimensionamento del lettore.

La Video Heartbeat Library (VHL) è stata aggiornata alla versione 1.5.9 per risolvere i seguenti problemi:

* Zendesk #23730 - Le metriche del bitrate sono vuote

Questo problema è stato risolto tenendo traccia delle modifiche del bitrate in VideoAnalyticsTracker.

* È stata aggiunta la nuova API assetDuration a PTVideoAnalyticsTrackingMetadata per aggiornare la durata della risorsa per i flussi live/lineari.

**Versione 1.4.28** (848)

* #25027 Zendesk - L’Auditude non funziona nella versione desktop 1.4.27

Il problema è stato risolto aggiungendo il codice per controllare AUDITUDE_METADATA_KEY e rendendo intercambiabili AUDITUDE_METADATA_KEY e ADVERTISING_METADATA_KEY.

* Zendesk #24428 - Problema di buffering frequente utilizzando TVSDK per riprodurre un DRM HLS

Questo problema è stato risolto tenendo conto che in assenza di configurazione degli annunci, TVSDK può velocizzare l’elaborazione eliminando il blocco pre-roll degli annunci e il blocco live booking sulla timeline progettata per sincronizzare l’inserimento degli annunci.

* Zendesk #24344: disabilita i file WebVTT per migliorare i tempi di avvio.

**Nota**: questo problema richiede Flash Player 23 o versione successiva.

Questo problema è stato risolto caricando i file WebVTT solo quando è necessario visualizzare i sottotitoli.

* Zendesk #24994 - I sottotitoli codificati vengono eliminati dal lettore al ritorno dalla pausa pubblicitaria

**Nota**: questo problema richiede Flash Player 23 o versione successiva.

Il codice EOC fittizio ha fatto scomparire la visualizzazione della didascalia. Questo problema è stato risolto obbligando i codici di didascalia 608 RU2, RU3 e RU4 a fornire la corretta visibilità nella finestra attiva corrente.

**Versione 1.4.27** (844)

* #21554 Zendesk - Beacon di errore TVSDK non attivati per il tipo di applicazione = video/mp4

Questo problema è stato risolto abilitando TVSDK a eseguire il ping degli URL di tracciamento degli errori corretti su formati di risorse non validi.

* Zendesk #23402 - Riproduzione annuncio incompleta

**Nota**: questo problema richiede Flash Player 23 o versione successiva.

Dopo aver ricevuto un errore 404 in alcune richieste, potrebbe verificarsi un arresto anomalo. Questo problema è stato risolto assicurandosi che la connessione non si arresti durante la gestione della risposta. La risoluzione assicura che i file degli annunci VPAID non vengano conteggiati in modo errato, pertanto non vengono rilasciati durante il download.

* #23621 Zendesk - Nuovo tentativo non riuscito su 400 e 404

**Nota**: questo problema richiede Flash Player 23 o versione successiva.

È stato risolto il problema che causava il danneggiamento dei metadati DRM quando si passava da un profilo all’altro.

* #23705 Zendesk - Blocco degli annunci video durante le interruzioni AdStitched

**Nota**: questo problema richiede Flash Player 23 o versione successiva.

Questo problema è lo stesso di Zendesk #23621.

* #23905 Zendesk - Alcune interruzioni pubblicitarie saltano le interruzioni pubblicitarie

**Nota**: questo problema richiede Flash Player 23 o versione successiva.

Il codice di rete nativo di Windows è stato corretto per garantire che le connessioni non chiudano gli handle attualmente utilizzati da altre connessioni.

* Ticket #24029 - I flussi HLS FER non riproducono tutti gli annunci mid-roll nel file .json mid-roll.

Questo problema è stato risolto consentendo ai client di impostare separatamente i parametri personalizzati nell’istanza Opportunity in modo che non debbano eseguire l’override di OpportunityGenerator.

**Versione 1.4.26** (839)

* Zendesk #18854 - Aggiorna la logica di selezione creativa in base alle regole CRS
   * Fornito il supporto per aggiornare la logica di selezione creativa in base alle regole CRS

* #22725 Zendesk - implementazione playbackManager.beginPlayback() nell’applicazione di esempio per desktop

   * È stato risolto rimuovendo questa chiamata ridondante alla fine di startPlaybackFromFlashVars, poiché il metodo viene chiamato da setupVideo()

* #22807 Zendesk - Eccezione riferimento null SeekManager

   * Risolto fornendo la necessaria protezione NULL del puntatore all’interno di SeekManager relativa a _dispatcher

* Zendesk #22822 - Buffering frequente quando si utilizza TVSDK per riprodurre un HLS chiaro

   * Risolto rimuovendo l’opportunità iniziale generata da adSignalingModeOpportunityGenerator se non è presente alcun annuncio

* #23378 Zendesk - L’integrità del flusso blocca rules.xml

   * Correzione tramite il caricamento del file rules.xml tramite il flusso di lavoro di integrità del flusso

**Versione 1.4.24** (817)

* Zendesk #19851 - Quando il lettore si adatta a un bit rate diverso, salta indietro di alcuni fotogrammi nel tempo sul nuovo bit rate, creando un’esperienza imbarazzante

**Nota**: questo problema richiede il lettore Flash 22.0.0.175 o versione successiva.

È stato risolto il problema relativo alla reimpostazione della scheda DRM dopo il download di una piccola frazione di un segmento che non viene ripristinata correttamente.

* Zendesk #20784 - Analytics: attivazione della completezza dei contenuti per le transizioni video live

Questo problema è stato risolto aggiungendo un’API (trackVideoComplete) per attivare manualmente il completamento del contenuto durante una sessione di tracciamento video LINEAR/LIVE.

Sono state aggiornate le seguenti librerie:

* #21643 Zendesk - Gli annunci VPAID non vengono riprodotti completamente

   * Libreria AdobeMobile alla versione 4.10.0
   * Libreria VHL alla versione 1.5.6
   * VHL-Nielsen alla libreria 1.6.7

Questo problema è stato risolto utilizzando un riquadro di visualizzazione a altezza zero per riempire la fase di riproduzione di un annuncio VPAID.

* #22110 Zendesk - Analytics: aggiungi un h:sc:campo ssl per le chiamate di tracciamento heartbeat

I problemi relativi a SSL sono stati risolti e la libreria VHL utilizzata in TVSDK è stata aggiornata alla versione più recente.

* Zendesk #22608 - Il video mostra a intermittenza uno schermo nero (richiede Flash Player 22.0.0.175 o versione successiva)

Durante il bitrate adattivo, con il limite massimo di bitrate, il ricaricamento del video mostra in modo intermittente una schermata nera anche se il client visualizza gli aggiornamenti alla posizione e si comporta come se il contenuto venisse riprodotto.

**Versione 1.4.23** (809)

* #2887 Zendesk - Problema di salto dell’annuncio post-roll quando la logica della regola annuncio viene applicata al TVSDK

**Nota**: questo problema richiede Flash Player 21.0.0.240 o versione successiva.

È stato risolto il problema a causa del quale gli annunci post-roll venivano ignorati quando la logica della regola dell’annuncio veniva applicata al TVSDK.

* #19863 Zendesk - Annuncio con file multimediale VPAID eliminato

Se un annuncio in linea di grandi dimensioni ha più file multimediali, con un annuncio VPAID come primo annuncio, l’annuncio in linea non viene riprodotto per i flussi live. Questo problema è stato risolto scegliendo un file multimediale diverso.

* Zendesk #21021 - Late Binding Audio (Audio associazione tardiva) che causa la ripetizione di segmenti audio

**Nota**: questo problema richiede Flash Player 21.0.0.240 o versione successiva.

Il problema di ripetizione audio è stato risolto.

* Zendesk #21125 - Ritorno dall&#39;annuncio live/lineare in anticipo

**Nota**: questo problema richiede Flash Player 21.0.0.240 o versione successiva.

Questa versione supporta il ritorno da un’interruzione pubblicitaria prima che l’interruzione pubblicitaria venga riprodotta fino al completamento. Il ritorno anticipato è indicato tramite un tag manifesto personalizzato.

* Zendesk # 21369 Late binding audio causa un tempo incoerente

**Nota**: questo problema richiede Flash Player 21.0.0.240 o versione successiva.

Questo problema è stato risolto anche dal problema di ripetizione audio che era stato risolto.

* Zendesk #21760, 20921 - Desincronizzazione audio-video su Seek.

**Nota**: questo problema richiede Flash Player 21.0.0.240 o versione successiva.

Il problema di ripetizione audio è stato risolto.

* #22024 Zendesk - Errore durante l’esecuzione di TVSDK

È stato risolto il problema a causa del quale il lettore di riferimento non riproduceva alcun flusso e generava un’eccezione all’avvio.

**Versione 1.4.22** (791)

* #17580 Zendesk - Errore di runtime Primetime con codice 3357

**Nota**: questo problema richiede Flash Player 21.0.0.197 o versione successiva.

Sono stati corretti gli errori casuali 3357 che si verificavano inizializzando correttamente deviceID quando viene chiamato storeVoucher().

* #21334 Zendesk - Valore di timeout della richiesta di annunci TVSDK per richieste di annunci di terze parti

In questa versione è stato aggiunto il timeout globale della richiesta dell’annuncio.

**Versione 1.4.21** (782)

* Zendesk #19580 TVSDK attende il completamento del resolver dei contenuti prima dell’invio `PTTimedMetadataChangedNotification` notifiche

**Nota**: questo problema richiede il lettore Flash 21.0.0.182 o versione successiva.

Questo problema è stato risolto in Lettore di riferimento desktop consentendo di impostare tag di annunci e aggiungendo un generatore di opportunità personalizzato che mostra come abbonarsi a suggerimenti personalizzati ed elaborare questi suggerimenti in un file VOD.

* Zendesk #20806 i futuri annunci mid-roll nella finestra DVR non si attiveranno dopo lo scambio di camme

**Nota**: questo problema richiede il lettore Flash 21.0.0.182 o versione successiva.

Questo problema è stato risolto aggiornando l’app per impostare _resource.metadata.setValue(DefaultMetadataKeys.ENABLE_LIVE_PREROLL, &quot;false&quot;) per disabilitare l’inserimento di annunci pre-roll in uno scambio PIP e, di conseguenza, non viene generata alcuna opportunità pre-roll.

È stata introdotta una funzionalità di ordinamento per correggere il posizionamento degli annunci fuori sequenza, che ha prodotto una durata negativa del contenuto principale.

* Zendesk #20522: impossibile saltare gli annunci VPAID 2.0

**Nota**: questo problema richiede il lettore Flash 21.0.0.182 o versione successiva.

* Questo problema è stato risolto saltando gli annunci VPAID durante il perdono degli annunci.
* Quando il criterio di interruzione dell’annuncio è impostato su Ignora, gli eventi di interruzione pubblicitaria e vengono ancora inviati. Lo stato del lettore non è coerente.

Questo problema è stato risolto per comportarsi correttamente e non inviare eventi quando l’interruzione pubblicitaria viene saltata.

* Zendesk #20955 Impostare coppie chiave-valore nella proprietà customParameters tramite il generatore di opportunità

**Nota**: questo problema richiede il lettore Flash 21.0.0.182 o versione successiva.

La richiesta di Auditude analizza le impostazioni Auditude per i parametri personalizzati durante la creazione di un’unità pubblicitaria per le richieste pubblicitarie.

Questo comportamento è stato modificato per includere nella richiesta parametri personalizzati dall’oggetto Opportunity. Inoltre, non è possibile comprimere più opportunità con parametri personalizzati diversi in una singola richiesta di Auditude.

* Zendesk #21227 - m3u8 non viene eseguito correttamente

**Nota**: questo problema richiede Flash Player 21.0.0.211 o versione successiva.

Questo problema è stato risolto consentendo a TVSDK di ignorare il manifesto (profili secondari HLS) che contiene il codec AC3 non supportato da TVSDK (surround).

**Versione 1.4.20** (762)

* Zendesk #19181 - Trick play veloce avanti per live point blocca il flusso.

**Nota**: questo problema richiede Flash Player 20.0.0.306 o versione successiva.

* Zendesk #19286 - Si è verificato un arresto anomalo del Flash Player durante la ricerca avanti e indietro in un flusso FER.

**Nota**: questo problema richiede Flash Player 20.0.0.306 o versione successiva.

Gli attacchi occasionali che si verificavano durante la ricerca in Google Chrome venivano risolti arrestando le query, se le query impiegavano troppo tempo per ottenere una risposta o se il socket veniva arrestato.

* #19305 Zendesk - Si riscontra una riproduzione discontinua durante la riproduzione di un flusso con discontinuità A/V.

**Nota**: questo problema richiede Flash Player 20.0.0.306 o versione successiva.

Questo problema è stato risolto segnalando un avviso.

* Zendesk # 19359 - Flash Player arrestato a causa della posizione dell&#39;attributo #EXT-X-FAXS-CM: nel manifesto a livello di set.

Questo problema è stato risolto quando #EXT-X-FAXS-CM tag viene visualizzato nella playlist superiore prima di singoli bitrate o segmenti nella playlist.

* Zendesk #19489 - Fast Forward to Live Point stalls plugin (streaming live)

Questo problema è lo stesso di Zendesk #19181.

* Zendesk #19699 - TVSDK non riesce a passare da una traccia di sottotitoli WebVTT a un&#39;altra

Questo problema è stato risolto effettuando il dump del lettore e ricaricando il manifesto quando un brano cambia e correggendo il problema di conversione delle stringhe UTF8 che interessava i nomi dei brani di didascalia WebVTT a doppio byte.

**Versione 1.4.19** (1.4.19,738)

* Zendesk #18234 - Il Flash Player si blocca durante la riproduzione dei flussi con stringhe Unicode in CC

Questo problema richiede il Flash Player FP 20.0.0.267 o versione successiva ed è stato risolto gestendo correttamente la stringa Unicode.

* Zendesk #18304 - Supporto Stream Integrity per gli annunci VPAID

Questa funzione richiede FP 20.0.0.267 di Flash Player o versione successiva ed è stata introdotta nella versione 1.4.19.

* Zendesk #18766 - Reference Player non è in grado di visualizzare caratteri Unicode non latini nei nomi dei brani CC

Questa funzione richiede il Flash Player FP 20.0.0.267 o versione successiva ed è stata corretta gestendo la stringa Unicode.

* Zendesk #18804 - Arresto anomalo del lettore in Firefox 42

Questo problema richiede FP Flash Player 20.0.0.235 o versione successiva ed è lo stesso problema di Zendesk #18723.

* #18864 Zendesk - Arresto anomalo del plug-in del Flash Player

Questo problema richiede FP Flash Player 20.0.0.235 o superiore ed è lo stesso di Zendesk #18723.

* #18998 Zendesk - Se le marche temporali audio e video non corrispondono, si è verificato un download infinito di segmenti in caso di discontinuità.

Questo problema è stato risolto ignorando il gap tra le marche temporali e la semplice riproduzione del contenuto scaricato.

* Zendesk #19093 - Gli annunci mid-roll possono essere guardati una sola volta con contenuti FER (Live e Full-Event Replay), ma non possono essere guardati di nuovo quando si inoltrano o si cercano oltre gli annunci

Nel selettore adPolicy predefinito di Primetime, se viene visualizzato un annuncio mid-roll, l’adBreak non viene spostato nella posizione cercata al termine di una ricerca. Per riprodurre nuovamente l’annuncio, dopo la ricerca, l’applicazione deve ignorare la funzione selectAdBreaksToPlay().

* Zendesk #19101 - Riavvolgimento in annunci Midroll irrisolti rimuove il posizionamento dell&#39;annuncio.

Questo problema è stato risolto consentendo al lettore di aggiornare l’ora playbackMetrics, l’ora minimumOpportunityTime e la timeline.

* #19102 Zendesk - Problemi relativi alla modalità FER e trucco

Questo problema richiede FP 20.0.0.267 di Flash Player o versione successiva ed è stato risolto impostando correttamente advertisingMetadata.adSignalingMode.

* #19175 Zendesk - A volte gli annunci preroll non vengono visualizzati la prima volta che il flusso viene riprodotto.

Questo problema è stato risolto aggiungendo una nuova API, adRequestTimeout, alle AuditudeSettings per un timeout della richiesta dell’annuncio. Ora gli utenti possono ignorare il timeout predefinito di richiesta dell’annuncio di 10 secondi.

**Versione 1.4.18** (1.4.18.722)

* Zendesk #3324 - La generazione di rapporti sugli annunci Primetime non tiene traccia delle interruzioni pubblicitarie quando non sono presenti annunci multimediali in una VMAP.

Quando un’interruzione pubblicitaria è vuota, non veniva eseguito il ping degli eventi di inizio e di tracciamento completo dell’interruzione pubblicitaria. Questo problema è stato risolto inviando ping di avvio dell’interruzione pubblicitaria su interruzioni pubblicitarie vuote, come ad esempio VMAP AdBreak, con un nodo AdSource valido.

**Versione 1.4.17** (1.4.17.702)

* #17168 Zendesk - I sottotitoli non vengono visualizzati per circa 10 secondi dopo l’attivazione della visibilità

Questo problema è stato risolto fornendo supporto per il tag EXT-X-MEDIA-TIME per i file di didascalia vtt.

* Zendesk #17983 - Se non si scaricano le chiavi per un manifesto, la riproduzione dell’intero manifesto non riesce

**Nota**: devi avere almeno FP Flash Player 19.0.0.245 o superiore.

Quando a volte si riproduce contenuto live, è possibile che nel manifesto siano presenti chiavi non valide (ad esempio, per i periodi di sospensione attività), ma che altri intervalli di tempo abbiano chiavi valide che verranno comunque riprodotte. In precedenza, quando non era possibile scaricare una chiave elencata in un manifesto, l’intero manifesto non riusciva. Ora, il manifesto ha esito negativo solo quando non è possibile scaricare tutte le chiavi elencate. Se alcune chiavi sono valide, ma alcune di queste non possono essere scaricate, il contenuto verrà riprodotto. Continueremo a fallire se tenteremo di riprodurre un segmento che richiede una chiave che non abbiamo.

* Zendesk #18554 - In alcuni casi, Stream Integrity riduce i cookie

**Nota**: devi avere almeno FP Flash Player 19.0.0.245 o superiore.

È stato corretto un bug nel codice di manipolazione dei cookie che poteva troncare i valori dei cookie.

**Versione 1.4.16** (1.4.16,684)

* Zendesk #3732 - Aggiunta del supporto per i proxy in Chrome per l’integrità dello streaming (richiede FP 19.0.0.207 di Flash Player o versione successiva)

Questo è un miglioramento.

* Zendesk #4244 - Problemi di streaming al passaggio del PTS

Questo problema è stato risolto rilevando il rollover e gestendo la discontinuità per tipo di payload e non in modo generico.

* Zendesk #4487 - Tracciamento del canale lineare dei contenuti

Questo problema è stato risolto inizializzando nuovamente il tracciamento heartbeat video durante una sessione di riproduzione con flusso lineare.

* #17427 Zendesk - Integrità del flusso di Adobe non funzionante tramite un proxy su Chrome (Win7) ()

**Nota**: la risoluzione richiede FP Flash Player 19.0.0.207 o versione successiva.

Questo problema è lo stesso di Zendesk #3732.

* #17907 Zendesk - Lag on pHLS Live Stream con Flash Player 19

**Nota**: la risoluzione richiede FP Flash Player 19.0.0.207 o versione successiva.

Questo problema è stato risolto gestendo i flussi live in cui i domini dei file TS cambiano quando si ricarica il manifesto live e i file vengono scaricati due volte.

* #17931 Zendesk - La riproduzione dei contenuti HLS con slate all’inizio non riesce

**Nota**: la risoluzione richiede FP Flash Player 19.0.0.207 o versione successiva.

Il problema è stato risolto gestendo i flussi senza audio nei primi 2 secondi del primo file TS.

* Zendesk #17934 - Errore di streaming live con Flash 19.0.0.185

**Nota**: la risoluzione richiede FP Flash Player 19.0.0.207 o versione successiva.

Il problema è stato risolto gestendo i flussi in tempo reale con intervalli di tempo tra i fotogrammi audio e video sui limiti del segmento.

* Zendesk #17973 - Ultimo Flash Player 19.0.0.185 arresti durante il mid-roll

**Nota**: la risoluzione richiede FP Flash Player 19.0.0.207 o versione successiva.

Il problema è stato risolto gestendo l’audio non mixato con l’inserimento di annunci mid-roll. (Si verifica l’interruttore parser e, in qualsiasi punto della riproduzione, il contenuto passa all’annuncio mid-roll, o al centro della riproduzione dell’annuncio e così via.)

* Zendesk #18049 - crash del Flash 19 con Firefox 42 beta

Questo problema è lo stesso di Zendesk #17973.

**Versione 1.4.15** (1.4.15,678)

* #4377 Zendesk: attiva l’evento AD_BREAK_SKIPPED quando salta un’interruzione pubblicitaria a causa dei criteri dell’annuncio.

La correzione consisteva nell’aggiungere AD_BREAK_SKIPPED se un annuncio viene saltato.

* Zendesk #4496 - Integrità del flusso: errore 102100 con reindirizzamenti a flussi tokenizzati.

È stato corretto il supporto per l’impostazione della proprietà AVNetworkConfiguration useCookieHeaderForAllRequests tramite TVSDK.

* Zendesk #17179 - Arresto anomalo del lettore di Flash su più modifiche SAP per contenuti crittografati.

È stato corretto un arresto anomalo durante la riproduzione di alcuni contenuti crittografati.

**Nota**: la correzione richiede Flash Player versione 19.0.0.200 o successiva.

* Zendesk #17499 - come non rimuovere i midroll dopo l&#39;orologio ma rimuovere preroll dal contenuto fer

È stato aggiunto un tipo ad AdBreakTimelineItem (AdBreakTimelineItem.placementType) in modo che AdPolicySelector possa restituire un criterio diverso per contenuti pre-roll, mid-roll e post-roll.

* Zendesk #17665 - Limitazione della larghezza di banda

È stato corretto rimuovere la logica per modificare la dimensione del buffer di destinazione sulla dimensione iniziale all’inizio del buffering.

**Versione 1.14.14** (1.4.14,771)

* Zendesk #17363 - Correggi la documentazione README per il lettore di riferimento

   * Chiarire le istruzioni per scaricare e installare playerglobal.swc.
   * Aggiungi le istruzioni per aggiornare la configurazione del progetto con una versione specifica di Flash Player.
   * Aggiorna la configurazione del progetto AdvertisingOverlay per utilizzare la versione minima del lettore.
   * Aggiorna la configurazione del progetto ReferenceCore per utilizzare la versione specifica del lettore 11.9

* Zendesk #17471 - Il lettore si blocca

Correzione parziale per un problema a causa del quale un annuncio non viene riprodotto dall’inizio dopo la ricerca.

* Zendesk #17496 - Podbuster non si risolve quando si cerca nuovamente nella finestra DVR

Fornisci parametri personalizzati per ogni interruzione pubblicitaria.

**Versione 1.4.13** (1.4.13,660)

* Zendesk #4037 - Nessun errore di profilo utilizzabile (richiede Flash Player 18.0.0.232 o versione successiva)

risolvere il problema di analisi dell’url quando il parametro query contiene &quot;http&quot;

* #4260 Zendesk - Il Flash Player 18 si arresta in IE11 (richiede il Flash Player 18.0.0.232 o successivo)

È stato corretto un arresto anomalo durante la riproduzione di video in modalità a schermo intero con IE11

* Zendesk #4262 - Il lettore Adobe Primetime si blocca su Windows 10 (richiede Flash Player 18.0.0.232 o versione successiva)

È stato corretto un arresto anomalo durante la riproduzione di video in modalità a schermo intero con FireFox su Windows.

* #4279 Zendesk - Inserimento di annunci TVSDK HLS - Problema di reindirizzamento 302 su iOS e desktop

È stato risolto un problema a causa del quale il tipo di un URL non veniva riconosciuto correttamente perché privo di estensione.

* Zendesk #4306 - Arresto anomalo del Flash Player quando si passa a schermo intero solo su Win (richiede Flash Player 18.0.0.232 o versione successiva)

È stato corretto un arresto anomalo durante la riproduzione di video in modalità a schermo intero su Windows.

* #4480 Zendesk - Eventi tag ID3 mancanti (richiede Flash Player 18.0.0.232 o versione successiva)

**1.4.12 **(1.4.12.656)

* #2751 Zendesk - CSAI e CRS | Miglioramento: gestisci gli elementi dinamici in determinati URL di file multimediali.

È stato aggiornato il servizio Creative Repackaging per gestire correttamente gli annunci con URL creativi dinamici.

* PTPLAY - 2114 - Supporto riproduzione MP4.

È ora supportata la riproduzione di base di contenuti MP4, inclusi riproduzione, pausa e ricerca.

I seguenti elementi richiedono il Flash Player 18.0.0.225 o superiore:

* #3992 Zendesk - Velocità TrickPlay aggiuntive.

TrickPlay ora accetta tassi superiori a 16x: +/- 32, +/-64 e +/-128.

* #3113 Zendesk - Arresto anomalo del plug-in del Flash Player

È stato corretto un arresto anomalo durante il tentativo di riprodurre un annuncio di reindirizzamento su Mac Firefox.

* #4037 Zendesk - Nessun errore di profilo utilizzabile
* Zendesk #4262 - Il lettore Adobe Primetime si blocca su Windows 10

È stato corretto un arresto anomalo in Windows Firefox durante la riproduzione a schermo intero.

**Versione 1.4.11** (1.4.11.648)

* Zendesk #1869 - Problema durante la modifica della dimensione del carattere (richiede il Flash Player 18.0.0.200)

Consente di utilizzare le dimensioni dei sottotitoli nel codice dei sottotitoli WebVTT.

* Zendesk #3113 - Arresto anomalo del plug-in del Flash Player (richiede il Flash Player 18.0.0.200)
* Zendesk #3268 - Desktop: il lettore video inizia a sfarfalliare dopo +- 40/50 secondi e inizia a diventare nero dopo +- 90 secondi (richiede il Flash Player 18.0.0.200)

Correzione di un bug video dell&#39;area di visualizzazione.

* #3670 Zendesk - Errore INVALID_PARAMETER in VOD durante la ricerca nel lettore di riferimento (richiede il Flash Player 18.0.0.200)

InvalidateProfiles in ThreadSeek quando viene rilevato un nuovo periodo.

* Zendesk #3896 - Arresto anomalo del Flash Player con Integrità di flusso impostata su ON su Chrome (richiede il Flash Player 18.0.0.200)

È stato corretto un arresto anomalo in modalità di rete nativa in pepe

* Zendesk #3905 - Il lettore TVSDK non si carica se è in hosting su CDN

Sono stati risolti i problemi che rilevavano il token con caratteri jolly quando pageDomain era diverso dal dominio swf.

**Versione 1.4.10** (1.4.10.642)

* Zendesk #3249 - Il lettore web TVSDK arresta il Flash su Firefox

È stato risolto un arresto anomalo del Flash Player occasionale con Firefox su Mac quando uno streaming, in riproduzione su un monitor esterno, passava a uno streaming con bitrate più elevato.(richiede il Flash Player 18.0.0.160)

* Zendesk #3268 - Desktop: il lettore video inizia a sfarfalliare dopo `+-` 40/50 secondi e inizia a diventare nero dopo `+-` 90 secondi

È stato risolto un problema su Mac Chrome a causa del quale il flusso iniziava a sfarfalliare e alla fine diventava nero. (richiede il Flash Player 18.0.0.161)

* #3304 Zendesk - VAST 3.0 `[ERRORCODE]` la macro non viene compilata

   * se l’annuncio in linea non è creativo, viene visualizzato il codice di errore 400.
   * `[ERRORCODE]` la macro verrà codificata in URL

* Zendesk #3601 - Richiesta miglioramento: Wrapper companion management

   * In TVSDK verrà visualizzato il componente wrapper che contiene le risorse (html, iframe o statiche ) che si chiudono al file in linea. ( se il file in linea non ne contiene uno per quella dimensione)
   * I wrapper accompagnati da risorsa, a meno che non vengano utilizzati per la visualizzazione, verranno ignorati. (non utilizzato per il tracciamento )
   * A scopo di tracciamento verranno utilizzati solo i wrapper companion senza alcuna risorsa. ( contenitore wrapper che contiene solo il tracciamento )

**Versione 1.4.9**

* #2615 Zendesk - problema durante la rimozione della visualizzazione HLS dallo schermo del desktop

Metodo clearVideo() aggiunto a MediaPlayer. Cancella il fotogramma video visualizzato cancellando AVStream dall&#39;oggetto StageVideo. Deve essere chiamato solo se il video è in pausa e replaceCurrentResource o replaceCurrentItem deve essere chiamato prima di poter chiamare nuovamente play().

* Zendesk #3169 - Aggiornare il lettore di riferimento con l’integrazione di Adobe Analytics

Il lettore di riferimento è stato aggiornato con l’integrazione con Adobe Analytics

* Zendesk #3296 - Desktop HLS TVSDK - VASTI annunci di terze parti non riprodotti

I tipi mime per il formato HLS facevano distinzione tra maiuscole e minuscole, era errato ed è stato modificato per cui non fanno più distinzione tra maiuscole e minuscole

**Versione 1.4.8**

* Zendesk #2737 - Lettore desktop - 106000 di errore (richiede Flash Player 17.0.0.184)
* Zendesk #3007 - Gli annunci pre-roll non vengono visualizzati dopo l’aggiornamento al Flash Player 17 (richiede il Flash Player 17.0.0.184)
* Zendesk #3085 - Il lettore HLS desktop genera 106000 errore dopo 60 secondi (richiede il Flash Player 17.0.0.184)

**Versione 1.4.7**

* #2760 Zendesk - Tag DISCONTINUITY ignorato durante la modalità TrickPlay (richiede la versione di Flash Player 17.0.0.158)
* #2760 Zendesk - Tag DISCONTINUITY ignorato durante la modalità TrickPlay (richiede la versione di Flash Player 17.0.0.158)

**Versione 1.4.6**

* Zendesk #2652 - Documentazione di Auditude per HLS desktop, Auditude chiarita di media_id per HLS desktop

**Versione 1.4.5**

* Zendesk #2256 - Accesso alla playlist principale, PSDK aggiornato per l’invio di eventi timedMetadata per i tag abbonati alla playlist principale. (richiede la versione di Flash Player 17.0.0.134)
* Zendesk #2417 - Lettore che stava tentando di scaricare i sottotitoli prima dell’inizio della riproduzione, WebVTT stava utilizzando la variabile del numero di segmento errata per la corrispondenza del numero di segmento. Il bug viene visualizzato solo per i file multimediali con indici di segmento a partire da zero. (richiede la versione di Flash Player 17.0.0.134)
* Zendesk #2537 - Il lettore di Flash si blocca quando si utilizza il plug-in pepe con Chrome (è richiesta la versione di Flash Player 17.0.0.134)
* Zendesk #2547 - Sottotitoli in arabo: il testo deve essere allineato con giustificazione a destra (richiede la versione del Flash Player 17.0.0.134)

**Versione 1.4.4**

* Zendesk #1561 - Ri: `[Adobe Primetime]` Aggiornamento: supporto del failover basato su client HLS per PROGRAM-DATE-TIME in Desktop PSDK (richiede la versione di Flash Player 16.0.0.305 o successiva)
* #2197 Zendesk - `[Ads]` Tracciamento degli errori pubblicitari
* Zendesk #2286 - Richiesta di funzioni: fornire informazioni sullo stato di caricamento degli annunci (VPAID)
* Zendesk #2285 - Richiesta funzionalità: ignora l’annuncio dopo una durata di timeout specificata
* Bug #3921755 - Aggiornamento della libreria OpenSSL alla versione 1.0.1L in Flash Player (richiede la versione di Flash Player 16.0.0.305 o successiva)

**Versione 1.4.2**

* Zendesk #1303 - Offset verticale per sottotitoli (richiede la versione di Flash Player 16.0.0.235 o successiva, data di rilascio prevista: dicembre 2014)
* Zendesk #1870 - Attivazione e disattivazione sottotitoli (richiede la versione del Flash Player 16.0.0.235 o successiva, data di rilascio prevista: dicembre 2014)
* Zendesk #2110 - La riproduzione si blocca dopo aver tentato di accedere allo schermo intero durante un annuncio VPAID (richiede la versione di Flash Player 16.0.0.235 o successiva, data di rilascio prevista: dicembre 2014)
* #2199 Zendesk - `[VPAID]` Il lettore non risponde quando cerca l’interruzione pubblicitaria passata
* Zendesk #2358 - Ri: `[Analytics]` Dati capitolo errati

**Versione 1.4.1**

* Aggiornamento dell’API di sospensione attività per coerenza con l’implementazione per Android e iOS.

**Versione 1.4.0**

* #1024 Zendesk - Funzione per rimuovere un annuncio dal flusso tramite manifesto
* Zendesk #1423 - Errore di riproduzione HLS durante il blocco del Flash Player (senza errori segnalati)
* Zendesk #1674 - ClosedCaption Non viene visualizzato, vengono visualizzati i sottotitoli 708 corretti quando mancano i codici ETX 0x03.

## Problemi noti {#known-issues}

* I sottotitoli codificati non funzionano con contenuti solo audio perché il sistema dei sottotitoli richiede un video per funzionare.
Senza video, non esiste alcuna dimensione del riquadro di visualizzazione e senza una dimensione del riquadro di visualizzazione non è possibile visualizzare elementi grafici per i sottotitoli.
* L’integrità del flusso è leggermente più lenta in Google Chrome a causa delle restrizioni relative alla sandbox di Chrome.
* In TVSDK 1.4, se si disattiva autoPlay, potrebbe verificarsi un errore DRM quando il lettore rimane inattivo per almeno un minuto. Per risolvere questo problema, se disattivi AutoPlay ma precarichi le risorse, modifica `ReferenceCore.as` modificando il contenuto di `onPlaybackManagerPrepared`:

```
if (_playbackManager.autoPlay) {
_playbackManager.play();
} else {
_playbackManager.play();
_playbackManager.pause();
}
```

* **Versione 1.4.13** PTPLAY-8501 - Quando VMAP restituisce due annunci MP4 diretti non transcodificati, lo stesso annuncio di fallback viene riprodotto due volte.

* **Versione 1.4.2** Nella versione 16 del Flash Player, è stato identificato un problema con la logica ABR di &quot;spegnimento&quot;, dopo che il lettore entra in un evento di buffering vuoto. Questo problema impedisce che il bitrate si disattivi in ambienti con larghezza di banda errata una volta che il lettore entra in uno stato di buffering. Per risolvere il problema, chiedi all’app di impostare il `BufferControlParameters.initialBufferTime` per essere uguale a `BufferControlParameters.playbackBufferTime` temporaneamente durante lo stato di buffering (ovvero su `BufferEvent.BUFFERING_BEGIN` ) quindi riportarlo ai valori impostati su `BufferEvent.BUFFERING_END` evento. La correzione per questo problema sarà disponibile nella prossima versione patch della versione 16 del Flash Player.

* **Versione 1.4.0**

   * PTPLAY-1634 - Lo stesso tag Abbonato ha marche temporali diverse in finestre live diverse. Quando si spostano le finestre live, lo stesso tag in ciascuna di esse deve avere gli stessi timestamp. Tuttavia, a volte gli stessi tag hanno marche temporali diverse.
   * PTPLAY-28 - La timeline di MediaPlayer non include interruzioni vuote.
   * È necessario un file dei criteri per più domini (crossdomain.xml) per consentire lo streaming del contenuto da un dominio diverso. [Impostazione di un file crossdomain.xml per il flusso HTTP](https://helpx.adobe.com/adobe-media-server/dev/configure-dynamic-streaming-live-streaming.html).
   * #3694203 bug: in un flusso DVR, la ricerca dall’interno di un mid-roll di riproduzione a un altro annuncio mid-roll può causare il blocco del browser
   * #3753725 bug: selectPolicyForSeekIntoAd non tiene conto se l’interruzione pubblicitaria è stata guardata
   * #3754529 bug: gli annunci pre-roll non vengono rimossi dal flusso durante il ripristino in un flusso DVR live
   * #3761896 bug: se la ricerca è consentita durante la riproduzione dell’annuncio, gli indicatori dell’annuncio si regolano nuovamente dopo la ricerca. La soluzione consiste nel non utilizzare il callback ITEM_UPDATED durante la ricerca
   * #3779889 bug: la chiamata completa non viene effettuata quando si raggiunge la fine nella riproduzione con trucco in Video Analytics
   * #VA-779 bug: l’heartbeat dell’evento di modifica del bitrate non viene inviato per Analisi video avanzata con supporto Heartbeat - Implementazione di riferimento: la riproduzione tramite token non viene implementata nell’applicazione di esempio.

## Risorse utili {#helpful-resources}

* Consulta la documentazione completa dell’Aiuto all’indirizzo [Informazioni e supporto per Adobe Primetime](https://helpx.adobe.com/support/primetime.html) pagina.
