---
title: Note sulla versione di TVSDK 1.4 per iOS
description: Le note sulla versione di TVSDK 1.4 per iOS descrivono le novità o le modifiche, i problemi risolti e noti e i problemi del dispositivo in TVSDK iOS 1.4
products: SG_PRIMETIME
topic-tags: release-notes
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '6549'
ht-degree: 0%

---

# Note sulla versione di TVSDK 1.4 per iOS {#tvsdk-for-ios-release-notes}

Le note sulla versione di TVSDK 1.4 per iOS descrivono le novità o le modifiche, i problemi risolti e noti e i problemi del dispositivo in TVSDK iOS 1.4.

## Nuove funzioni {#new-features}

**Versione 1.4.45**

* Al fine di rispettare Xcode10, TVSDK è stato spostato da &quot;`libstdc++`&quot; a &quot;`libc++`&quot;, e di conseguenza la versione minima supportata è iOS 7. In precedenza era iOS 6.

**Versione 1.4.44**

* Nessuna nuova funzione o miglioramento in questa versione.

**Versione 1.4.43**

* Esperienza simile alla TV, ovvero essere in grado di iscriversi nel mezzo di un annuncio senza attivare il tracciamento parziale dell’annuncio.\
  Esempio: l’utente si unisce al centro (a 40 secondi) di un’interruzione pubblicitaria di 90 secondi composta da tre annunci di 30 secondi. Questo è a 10 secondi dal secondo annuncio nell’interruzione.

   * Il secondo annuncio viene riprodotto per la durata rimanente (20 secondi) seguito dal terzo annuncio.
   * I tracker degli annunci per l’annuncio parziale riprodotto (secondo annuncio) non vengono attivati. Vengono attivati i tracker solo per il terzo annuncio.

* Aggiunta della proprietà enableVodPreroll di tipo booleano nell&#39;interfaccia PTAdMetadata. La proprietà può essere utilizzata per abilitare il pre-roll su un flusso VoD. Se enableVodPreroll è NO, PSDK non riproduce il pre-roll. Questo, tuttavia, non ha alcun impatto sui midrolls. Il valore predefinito di enableVodPreroll è YES.
* l&#39;API closedCaptionDisplayEnabled dell&#39;interfaccia PTMediaPlayer è contrassegnata come obsoleta a partire dalla versione 1.4.43 di iOS. Per determinare se i sottotitoli codificati sono disponibili per un determinato elemento PTMediaPlayerItem, esaminare la proprietà subtitlesOptions di PTMediaPlayerMediaItem.

**Versione 1.4.42**

Non vengono aggiunte nuove funzioni in questa versione. Per un elenco dei problemi risolti, vedi Problemi risolti.

**Versione 1.4.41**

Modifiche API:

* **isSecure**: viene introdotta una nuova API isSecure per proteggere il lettore dalla registrazione e dalla generazione di un errore. Il valore predefinito è true.
* **allowExternalRecording**: viene introdotta una nuova API per consentire il mirroring airplay di un contenuto sicuro. Il mirroring airplay viene trattato come registrazione, pertanto il valore allowExternalRecording deve essere impostato su &quot;True&quot; per consentire il mirroring airplay o su &quot;False&quot; per arrestare il mirroring airplay per un contenuto sicuro. Per impostazione predefinita, il valore è true.

**Versione 1.4.40**

Nessuna nuova funzione.

**Versione 1.4.39**

* iOS TVSDK è certificato con VHL 2.0.1 e con VHL 2.0.1 con Nielsen.
* iOS TVSDK è stato aggiornato per effettuare richieste CRS dal nuovo host Akamai `primetime-a.akamaihd.net`.
* La nuova configurazione del nome host fornisce la distribuzione delle risorse CRS tramite HTTP e HTTPS (SSL) su scala più ampia.

**Versione 1.4.36**

Integrare e certificare VHL 2.0 in iOS TVSDK : riduce la barriera nell’implementazione di VideoHeartbeatLibrary diminuendo la complessità delle API.

**Versione 1.4.34**

* Informazioni sugli annunci di rete

  Le API TVSDK ora forniscono informazioni aggiuntive sulle risposte VAST di terze parti. L’ID annuncio, il sistema di annunci e le estensioni VAST per annunci sono forniti in `PTNetworkAdInfo` classe accessibile tramite  `networkAdInfo`  su una risorsa annuncio. Queste informazioni possono essere utilizzate per l’integrazione con altre piattaforme Ad Analytics come **Moat Analytics**.

**Versione 1.4.31**

* **Metriche di fatturazione** Per soddisfare i clienti che desiderano pagare solo per ciò che utilizzano, anziché una tariffa fissa indipendentemente dall’uso effettivo, Adobe raccoglie le metriche di utilizzo e le utilizza per determinare quanto fatturare ai clienti.

Ogni volta che TVSDK genera un evento di avvio del flusso, il lettore inizia a inviare periodicamente messaggi HTTP al sistema di fatturazione di Adobe. Il periodo, noto come durata fatturabile, può essere diverso per VOD standard, pro VOD (annunci mid-roll abilitati) e contenuti live. La durata predefinita per ogni tipo di contenuto è di 30 minuti, ma il contratto con Adobe determina i valori effettivi.

* **Supporto multi-CDN per annunci CRS** TVSDK ora supporta Multi-CDN per gli annunci CRS. Specificando i dettagli FTP per gli annunci CRS, puoi specificare posizioni CDN diverse dalla CDN di proprietà dell’Adobe predefinita, ad esempio Akamai.

**Versione 1.4.29**

Nella classe PTSDKConfig è stata aggiunta l&#39;API forceHTTPS.

La classe PTSDKConfig fornisce metodi per applicare SSL alle richieste effettuate ai server Adobe Primetime ad decisioning, DRM e Video Analytics. Per ulteriori informazioni, vedere `forceHTTPS` e `isForcingHTTPS` metodi in questa classe. Se un manifesto viene caricato su HTTPS, TVSDK mantiene l’utilizzo del contenuto di HTTPS e rispetta tale utilizzo durante il caricamento di eventuali URL relativi da tale manifesto.

**Nota**: le richieste a domini di terze parti come pixel di tracciamento degli annunci, URL di contenuti e annunci e richieste simili non vengono modificate ed è responsabilità dei provider di contenuti e dei server di annunci fornire URL supportati tramite HTTPS.

**Versione 1.4.18**

Primetime iOS TVSDK ora supporta i creativi JavaScript VPAID 2.0 per consentire un’esperienza pubblicitaria interattiva in-stream avanzata.

Per ulteriori informazioni su VPAID 2.0, vedere [Supporto per annunci VPAID](../programming/tvsdk-1.4-for-ios/ad-insertion/c-psdk-ios-1.4-vpaid-2.0-ads.md).

**Versione 1.4.17**

* tvOS

  TVSDK supporta le applicazioni native tvOS.
* È possibile riprodurre i seguenti tipi di contenuto:

   * VOD
   * Live
   * AES-128
   * Audio alternativo e sottotitoli
   * FER

* È possibile visualizzare i seguenti tipi di annunci:

   * Base
   * VAST2
   * VAST3
   * VMA

* Le seguenti funzioni non sono attualmente supportate:

   * Digital Rights Management (DRM)
   * Banner pubblicitari
   * Linguaggio di markup TV (TVML)

**Versione 1.4.13**

**Nota**: il modulo Nielsen è stato rimosso dalla build TVSDK, il TVSDK verrà aggiornato a breve con un nuovo modulo di integrazione Nielsen.

* **Fallback degli annunci, concatenamento a margherita nella logica di selezione degli annunci (#3103 Zendesk)**

Per gli annunci VAST (creativi) con la regola di fallback abilitata, TVSDK tratta un annuncio con un tipo MIME non valido come annuncio vuoto e tenta di utilizzare gli annunci di fallback al suo posto. Puoi configurare alcuni aspetti del comportamento di fallback.

Per ulteriori informazioni, consulta [Fallback degli annunci per annunci VAST e VMAP](../programming/tvsdk-1.4-for-ios/ad-insertion/c-psdk-ios-1.4-ad-fallback.md).

**Versione 1.4.9**

* **Segnalazione Di Sospensione Attività Con Sostituzione Contenuti Alternativa**

Come parte dell’aggiornamento 1.4 di TVSDK, ora supportiamo anche l’accesso e il ritorno da blackout regionali rispetto ai contenuti lineari. TVSDK è ora in grado di elaborare due file manifest in parallelo, principale e alternativo, per monitorare i segnali di blackout anche quando viene mostrata una programmazione alternativa al posto della programmazione originale.

**Versione 1.4.8**

* **Video Heartbeats Library (VHL) aggiornato alla versione 1.5**

   * Possibilità di inviare metadati con avvio video e/o inizio video/annuncio/capitolo come dati contestuali
   * Traffico di rete ridotto: gli heartbeat sono in media meno numerosi e di dimensioni più ridotte

**Versione 1.4.7**

* **Supporto per la personalizzazione on-premise**

Supporto per le installazioni on-premise di Adobe Individualization Server per personalizzare la richiesta di personalizzazione del client in modo da passare a un endpoint diverso.

* **Protezione dell&#39;output basata sulla risoluzione**

I criteri DRM possono ora specificare la risoluzione massima consentita, a seconda delle funzionalità di protezione dell&#39;output del dispositivo. Ad esempio, &quot;Se è disponibile HDCP, è possibile riprodurre contenuti con risoluzione fino a 1080p e, se non è disponibile HDCP, è possibile riprodurre contenuti con risoluzione fino a 480p&quot;.

**Versione 1.4.4**

* **Aggiornamento Video Heartbeats Library (VHL) alla versione 1.4.1.1**

   * Con Adobe Analytics Video Essentials è stata aggiunta la possibilità di unire diversi casi di utilizzo di analisi da altri SDK o lettori.
   * Il tracciamento degli annunci è stato ottimizzato rimuovendo i metodi trackAdBreakStart e trackAdBreakComplete. L’interruzione pubblicitaria viene dedotta dalle chiamate dei metodi trackAdStart e trackAdComplete.
   * La proprietà della testina di riproduzione non è più necessaria durante il tracciamento degli annunci.
   * È stato aggiunto il supporto per l’ID visitatore del Marketing Cloud.

* **Integrazione di Nielsen SDK**

   * TVSDK ora supporta l’invio di beacon mTVR e MDPR ID3 all’SDK Nielsen senza alcuna integrazione personalizzata. Per iniziare, scarica l’SDK per app Nielsen iOS 3.1.2.19.

**Versione 1.4.0**

* **Segnalazione Di Sospensione Attività Con Sostituzione Contenuti Alternativa**

   * Come parte dell’aggiornamento 1.4 TVSDK, ora TVSDK supporta anche l’entrata e la restituzione da blackout regionali rispetto ai contenuti lineari. TVSDK è ora in grado di elaborare due file manifest in parallelo, principale e alternativo, per monitorare i segnali di blackout anche quando viene mostrata una programmazione alternativa al posto della programmazione originale.

* **Rimuovi/Sostituisci annunci C3**

   * Ora non è necessario alcun lavoro di preparazione aggiuntivo per inserire dinamicamente nuovi annunci nelle risorse video on demand (VOD) che escono dalla finestra C3. TVSDK ora fornisce un’API per rimuovere intervalli di contenuti personalizzati e inserire dinamicamente nuovi annunci. Questa nuova potente funzionalità è utile anche nei casi in cui i contenuti live/lineari vengano trasmessi durante la trasmissione e vengono immediatamente abbassati per essere utilizzati come contenuti on-demand senza il tempo necessario per &quot;ripulire&quot; la risorsa.

## Certificazione e supporto dei dispositivi in 1.4 {#device-certification-and-support-in}

>[!NOTE]
>
>Le seguenti funzioni sono **non** supportati in TVSDK:
>
>* Slow motion, su qualsiasi piattaforma o versione.
>* Gioco di trucco dal vivo.

**Versione 1.4.43**

* TVSDK 1.4.43 è certificato per iOS 11.

**Versione 1.4.29**

* TVSDK 1.4.29 è stato certificato per iOS 10.

**Versione 1.4.28**

* TVSDK 1.4.28 è stato certificato per iOS 10 Beta 7.
* Supporto DRM per forzare HTTPS aggiungendo le API forceHTTPS e isForcingHTTPS.
* Le librerie VHL sono state aggiornate alla versione 1.5.8, le librerie Adobe Mobile alla versione 4.8.4 e la libreria dell’utility logger alla versione 7.0.

**Versione 1.4.19**

Questa versione di TVSDK è stata certificata con il supporto FairPlay per iOS e tvOS.

**Versione 1.4.17**

* tvOS

  Questa versione di TVSDK include il supporto per tvOS ed è stata certificata per i flussi HLS non crittografati.

  **Nota**: ricorda le seguenti linee guida per la compilazione:

   * Il supporto per TVSDK tvOs è limitato ai flussi crittografati DRM non Adobi. È necessario rimuovere il riferimento a drmNativeInterface.framework nelle impostazioni di build di tvOS. I flussi crittografati AES sono ancora supportati.
   * Apple richiede che tutte le applicazioni Apple TV siano abilitate per il codice bit, pertanto è necessario attivare questo flag nelle impostazioni del progetto.

## Problemi risolti in 1.4 {#resolved-issues-in}

<!-- 

Comment Type: draft

 <p>All TVSDK customers who use CRS are strongly encouraged to upgrade to TVSDK 1.4.39 or latest on iOS and Android. This upgrade is a drop-in replacement to the existing app implementation. After the upgrade, check for the CRS creative URL requests in a proxy tool (for example, Charles) to verify that the version in the path reflects version 3.1. For example:</p> 
 <p><span class="code">https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/ 167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784bf3586d.m3u8</span></p> 
-->

<!-- 

Comment Type: draft

 <p>TVSDK versions earlier than version 1.4.28 sometimes exhibit a long delay in the startup time when ad-enabled content is played on devices that are running on iOS 10. To resolve this issue, upgrade to version 1.4.28 or later. Version 1.4.28 was released on August 31, 2016, and iOS 10 was released on September 13, 2016.</p> 

-->

**Versione 1.4.45{#ios-tvsdk}**

* Ticket #36294 - iOS TVSDK non funziona con Xcode 10

   * Sono stati risolti i problemi di compilazione con TVSDK su XCode 10. A causa dei requisiti Xcode 10, le app basate su TVSDK per iOS 1.4.45 e versioni successive richiedono un target di distribuzione minimo come iOS 7.0

* Ticket #36321 - Discrepanza osservata nell&#39;intervallo ricercabile tra l&#39;istanza PTMediaPlayer e AVPlayer nello stato &quot;Riproduzione&quot;.
* #36493 ticket - `libstdc++` supporto per iOS 12

   * Sono stati risolti i problemi di compilazione con TVSDK su iOS 12. Le app basate su TVSDK per iOS a partire dal 1.4.45 richiedono un target di distribuzione minimo come iOS 7.0

**Versione 1.4.44**

* Ticket #34683 - Il Tempo Di Avanzamento Della Riproduzione Dell’Annuncio Sta Diventando Negativo

   * Controlli aggiuntivi effettuati per gestire il caso in caso di mancata corrispondenza tra la durata segnalata dal server di annunci e il contenuto effettivo dell’annuncio.

* Ticket #34801 - currentTime e localTime non venivano aggiornati quando si cercava una nuova posizione durante lo stato di pausa

   * L’ora corrente del lettore può ora essere impostata su zero nel caso in cui il lettore sia in stato di pausa; prima l’ora corrente veniva impostata su zero solo in stato di riproduzione.

* Ticket #35037 - La riproduzione si interrompe con un URL errato al ritorno dall’inserimento di annunci basati sul segnale.

   * È stata migliorata la correzione fornita per il #34385 del problema chiuso nella versione 1.4.42. È stato aggiunto il codice di gestione degli assegni e delle eccezioni isCanceled per rendere più solida la coda delle operazioni.

**Versione 1.4.43**

* (ZD#32990) - iOS: riproduzione di contenuti invece di annunci su alcuni cue-point. L&#39;API &#39;selectedMediaOptionInMediaSelectionGroup&#39; che faceva parte dell&#39;interfaccia AVPlayerItem è ora stata spostata in AVMediaSelection in iOS 11. Il problema è stato risolto utilizzando questa nuova API.
* (ZD#33683) TVSDK ha rimosso == suffisso dalle stringhe di metadati. Il problema è risolto nella logica di analisi.
* (ZD#33905) - iOS TVSDK effettua chiamate ai file manifest con due agenti utente. Il problema dell’agente utente è stato risolto nella prima chiamata m3u8 (nuovo caso di installazione). M3u8 ha ora gli stessi agenti utente per tutte le chiamate.
* (ZD#34293) - I pre-roll inseriti nei flussi LINEAR non vengono riprodotti correttamente in iOS11. Il problema è risolto per gli annunci preroll.
* (ZD#34684) - Quando si applica il criterio di salto dell’annuncio, vengono visualizzati per alcuni secondi i fotogrammi degli annunci pre-roll. È stata introdotta una nuova API, enableVodPreroll, per disattivare la riproduzione preroll nella riproduzione vod. Il valore predefinito per questa API è &quot;Yes&quot;. L’API garantisce che l’unione dei contenuti degli annunci nel contenuto principale venga ignorata.
* (ZD#34765) - Dopo aver chiamato stop(), pochi segmenti Transport Streams vengono ancora scaricati. È stata migliorata l’API Stop() per evitare il download dei segmenti aggiuntivi.
* (ZD#34865) - Gli annunci pre-roll per livestream vengono troncati su iOS. Correlato a iOS11, e aggiungendo un controllo aggiuntivo per verificare se il flusso è pre-roll o main-content, risolve questo problema.
* (ZD#35093) - È stato corretto uno scenario di failover in cui, se la variante primaria del flusso non riesce all’avvio (restituisce 404), la riproduzione non passa al flusso di backup.

**Versione 1.4.42 (1.4.42.118)**

* (ZD#34385) - La riproduzione si interrompe con un URL errato al ritorno dall’inserimento di annunci basati sul segnale.

  Aumentare il numero massimo di operazioni simultanee per CustomAVAssetLoaderOperations, in modo che le letture del manifesto possano continuare a essere eseguite.
* (ZD#34373) - Gli utenti finali non sono in grado di effettuare lo streaming su dispositivi connessi tramite HDMI, quando la registrazione in streaming non è consentita.
* (ZD#32678) - TVSDK non raccoglie gli ID annuncio corretti su iOS.

  L’ID annuncio della creatività finale dell’annuncio viene ora rilevato nei ping VHL nel caso di reindirizzamenti VAST/VMAP.
* (ZD#33904) - TVSDK non è registrato per le notifiche AVFfoundation AVAudioSessionMediaServicesWereLostNotification e AVAudioSessionMediaServicesWereResetNotification.

  È ora possibile registrare PTMediaServicesWereLostNotification e PTMediaServicesWereResetNotification sull&#39;app del lettore per ottenere le notifiche quando i servizi multimediali vengono reimpostati o persi.

* (ZD#33815) - I clienti non possono aggiornare le regole CRS di definizione delle priorità e normalizzazione senza richiedere un aggiornamento dell’app.

  Sono state aggiunte le API getCRSRulesJsonURL e setCRSRulesJsonURL a iOS TVSDK.

**Versione 1.4.41 (1.4.41.76)**

* (ZD #34464) - Problemi durante la creazione dell’app di riferimento con TVSDK versione 1.4.41

  A partire da questa versione, è necessario Xcode 9 per compilare TVSDK per iOS.
* (ZD #29456) - Avvio dell’esecuzione in pausa

  È stato risolto il problema relativo alla pausa che si verificava quando il video veniva messo in pausa durante l’accesso a Airplay.
* (#30371 ZD) - L’ora di inizio dell’AdBreak cambia quando inseriamo più di 2 annunci in streaming lineare

  È stato corretto l’errore che si verificava durante il tentativo di riproduzione di contenuto su Apple TV, che impediva la riproduzione completa
* (#32146 ZD)- Non viene ricevuto PTMediaPlayerStatusError per il contenuto HLS Live quando si blocca iOS 11 dev beta

  Non è stato ricevuto alcun PTMediaPlayerStatusError per i contenuti HLS Live e VOD al momento del blocco tramite Charles (connessione diretta e 403)
* (ZD #29242) - Riproduzione video Airplay non riuscita con annunci abilitati

  Quando gli annunci sono abilitati e AirPlay è abilitato all’avvio della riproduzione di un video, la riproduzione del video non inizia mai e non viene visualizzato alcun errore
* (ZD#33341) - DRMInterface.h attiva gli avvisi di generazione in Xcode 9

  Sono stati corretti due prototipi di blocchi in DRMInterface.h a cui mancava la parola &quot;void&quot; nei rispettivi elenchi di parametri
* (ZD#31979) - Non viene compilato/eseguito quando si utilizza iOS 10 o versione successiva per iPhone 7/iPhone7+

  La compilazione fissa di documenti IB per precedenti a iOS 7 non è più supportata
* (ZD#32920): schermata vuota all’interno di un’interruzione pubblicitaria e nessun completamento di interruzione pubblicitaria

  Quando un’interruzione pubblicitaria presenta istanze di annunci e al termine di un’istanza pubblicitaria, viene visualizzata una schermata vuota
* (ZD#32509) - Disabilita la registrazione schermo in iOS 11 Disabilita la registrazione schermo in iOS 11

* (ZD#33179) - Errore evento intermittente in iOS11

  È stato corretto l’errore dell’evento in iOS 11

**Versione 1.4.40** (1.4.40.72)

* (#32465 ZD) - Impossibile gestire le playlist unite.

  Chiamare finishLoadingWithError(with: Error) per consentire a AV Foundation di provare flussi alternativi/attivare il failover.

* (#31951 ZD) - Errore TVSDK durante la rotazione della licenza.

  È stato risolto il problema relativo alla rotazione delle licenze.
* (#31951 ZD): schermata vuota all’interno di un’interruzione pubblicitaria e nessun completamento di interruzione pubblicitaria.

  È stato risolto un problema a causa del quale gli annunci Facebook VPAID spesso restituivano più blocchi CDATA in un singolo nodo \&amp;lt;AdParameters\&amp;gt; VAST.
* (ZD #33336) - [iOS] TVSDK - I pod degli annunci non vengono riempiti, nonostante un numero sufficiente di annunci vengano restituiti dalla ruota libera.

  È stata creata una relazione padre-figlio tra l&#39;annuncio di sequenza e l&#39;annuncio di fallback e l&#39;ordinamento in base alla sequenza e all&#39;indice padre.

**Versione 1.4.39** (1.4.39.43)

* (#32178 ZD) - La versione di iOS TVSDK non è corretta.

  L’output della versione TVSDK nei file di registro era 1.0.211. È fisso per generare la versione corretta.

* (#32199 ZD) - Caricamento di annunci lazy - Il video non viene visualizzato per il contenuto.

  La timeline dell’interruzione di sessione locale che non veniva inizializzata in precedenza viene ora aggiornata prima dell’utilizzo.

* (#27528 ZD) - Video, audio o entrambi si bloccano 1-45 secondi dopo l’avvio della riproduzione di una risorsa, se l’audio secondario è impostato su non predefinito in iOS 1.2.

  Preparare e informare le tracce audio in stato Pronto.

* (#30411 ZD) - Se scegli una lingua Sap secondaria, potresti ottenere risultati imprevisti come assenza di audio o audio errato.

  Preparare e informare le tracce audio in stato Pronto.

* (#32199 ZD) - Caricamento di annunci lazy - Il video non viene visualizzato per il contenuto.

  La timeline dell’interruzione di sessione locale che non veniva inizializzata in precedenza viene ora aggiornata prima dell’utilizzo.

* (#27528 ZD) - Video, audio o entrambi si bloccano 1-45 secondi dopo l’avvio della riproduzione di una risorsa, se l’audio secondario è impostato su non predefinito in iOS 1.2.

  Preparare e informare le tracce audio in stato Pronto.

* (#30411 ZD) - Se scegli una lingua Sap secondaria, potresti ottenere risultati imprevisti come assenza di audio o audio errato.

  Preparare e informare le tracce audio in stato Pronto.

**Versione 1.4.38** (1.4.38,860)

* (ZD #29281) - iOS: aggiunta di AdSystem e Creative Id alle richieste CRS

Utilizzo di ID creativi e AdSystem nella richiesta CRS in base alle regole di normalizzazione CRS

* (#29176 ZD) - Arresto anomalo di PTAdPolicyDeligate satAdBreakAsWatched:position

Ora viene gestito l’arresto anomalo a causa di un AdBreak vuoto.

* (#30125 ZD) - Gli annunci programmatici non funzionano nella piattaforma iOS

È stato aggiunto il supporto per annunci programmatici in iOS.

* (ZD #30782) - Notifica #EXT-X-PROGRAM-DATE-TIME

L&#39;evento metadati temporizzati non viene attivato per il tag # EXT-X-PROGRAM-DATE-TIME con flussi LIVE DRM.

**Versione 1.4.37 (1.4.37.842)**

* (#28950 ZD ) - Problema di riproduzione VOD

Problema di riproduzione quando il tag # EXT-X-PLAYLIST-TYPE nel flusso è impostato su Event (Evento) anziché VOD

* (ZD #29281) - iOS: aggiunta di AdSystem e Creative Id alle richieste CRS

Utilizzo di Creative Id e AdSystem nelle richieste CRS in base alle regole di normalizzazione CRS.

* (#29462 ZD) - Annuncio TremorHub in VOD di A&amp;E che causa un arresto anomalo nelle app iOS

**Versione 1.4.36 (1.4.36.835)**

* (#29418 ZD) - Le cause con durata 0 (#EXT-X-CUE-OUT:0.000) causano l’arresto o l’arresto anomalo della riproduzione da parte di iOS TVSDK.

Il problema è risolto e la riproduzione viene avviata correttamente.

* (#29462 ZD) - L’annuncio in VOD causa un arresto anomalo su iOS TVSDK .

Il problema è risolto. iOS TVSDK sta generando un’eccezione (AUDNetworkAdInfo::initWithAdId) e non la sta gestendo. L’eccezione è dovuta a un ID annuncio vuoto.

* (ZD #29281)- Aggiungere AdSystem e Creative ID alle richieste CRS.

Includi AdSystem e CreativeId come nuovi parametri nelle richieste 1401 e 1403 (tutti gli altri parametri rimangono gli stessi).

**Versione 1.4.35** (1.4.35,830)

* (#27830 ZD) - È necessario determinare a livello di programmazione la differenza tra sottotitoli e sottotitoli in iOS.

TVSDK ora espone i due tipi che possono essere utilizzati per filtrare il tipo di didascalia richiesto.

* (#29160 ZD) - I cue degli annunci EXT-X-CUE-OUT non vengono uniti correttamente in TVSDK iOS.

Con EXT-X-CUE-OUT l’annuncio midroll viene riprodotto ora.

* (#29100 ZD) - L’app si blocca quando l’utente scorre fino alla fine di un filmato.

Sono stati risolti diversi arresti anomali relativi alla sincronizzazione.

* (#28785 ZD), (#27712 ZD) e (#25076 ZD) - L’app iOS subisce un arresto anomalo durante i grandi eventi live.

Sono stati risolti diversi arresti anomali relativi alla sincronizzazione.

**Versione 1.4.34** (1.4.34.815 per iOS 6.0+)

* (ZD# 28481) - Interruzione FER a causa della aggiunta di una chiave errata al termine di un’interruzione pubblicitaria per tali flussi FER

Per un flusso FER, la chiave prima dell’interruzione pubblicitaria viene inserita dopo la fine dell’interruzione pubblicitaria. Questo problema è stato risolto aggiungendo *ultima chiave visualizzata* alla fine dell’interruzione pubblicitaria.

**Versione 1.4.33** (1.4.33.803 per iOS 6.0+)

* (ZD# 21701) Abilita CRS per i conti secondari

Abilitato inviando l’URL creativo originale per la richiesta 1401 CRS invece dell’URL normalizzato, in base al requisito per il back-end CRS.

* (ZD# 26218) - Problema di caricamento di PSDKResources.bundle

Questo problema è stato risolto aggiornando il caricamento delle risorse in modo che vengano visualizzate da tutti i bundle disponibili.

* (ZD# 27460) Prima chiamata annuncio Midroll - Da POST a cdn.auditude<span></span>.com restituisce 403.

Il nuovo account CDN non è in grado di gestire una richiesta CDN di POST. Questo problema è stato risolto aggiornando il codice per rendere `cdn.auditude.com` richiesta annuncio da GET anziché POST.

**Versione 1.4.32** (1.4.32.792 per iOS 6.0+)

* (ZD# 27132) Supporto per i valori decimali per le interruzioni pubblicitarie VMAP.

Quando il contenuto non veniva segmentato lungo le interruzioni pubblicitarie definite, i numeri interi causavano posizionamenti di annunci imprevisti. Il problema è stato risolto non convertendo i valori decimali in numeri interi.

* (ZD# 27189) I contenuti AES con il tag EXT-X-DISCONTINUITY-SEQUENCE non vengono riprodotti correttamente.

Il problema è stato risolto inserendo il tag all’inizio della playlist.

**Versione 1.4.31** (1.4.31.785 per iOS 6.0+)

* (ZD# 24528) Implementazione delle metriche di utilizzo TVSDK per la fatturazione

Per ulteriori informazioni, consulta [Metriche di fatturazione](../programming/tvsdk-1.4-for-ios/c-psdk-ios-1.4-billing/c-psdk-ios-1.4-billing.md).

* (ZD# 24642) Supporto Picture-in-Picture per TVSDK

La funzione picture-in-picture, che in alcuni casi non funzionava correttamente, è stata corretta.

* (ZD# 25246) Segnali di interruzione annuncio non corretti

Questo problema è stato risolto allineando i tag di discontinuità tra i manifesti delle varianti.

* (ZD# 26218) Il processo di compilazione dell&#39;applicazione si complica quando si tenta di includere PSDKLibrary.framework nel framework dell&#39;applicazione del client

Questo problema è stato risolto creando il pacchetto PSDKLibrary.framework come richiesto.

* (ZD# 26364) Supporto multi-CDN per annunci CRS
<!-- 
Comment Type: draft
For more information, see [Multiple CDN support for CRS Ad Delivery](http://help.adobe.com/en_US/primetime/psdk/ios/1.4/index.html#PSDKs-concept-Multiple_CDN_support_for_CRS_ad_delivery).
-->
* (ZD# 27028) Ritardo nella riproduzione di alcuni flussi in iOS 10.

Questo problema è stato risolto fornendo una soluzione alternativa per i flussi che non hanno un’estensione M3U8.

**Versione 1.4.30** (1.4.30.754 per iOS 6.0+)

In questa versione sono stati risolti i seguenti problemi per TVSDK:

* (ZD# 24180) Aggiungi un’intestazione personalizzata all’elenco consentiti

È stata aggiunta una nuova intestazione personalizzata all’elenco consentiti TVSDK.

* (ZD# 25016) Il flusso di failover viene selezionato in modo casuale quando vengono impostati i parametri di controllo ABR

Questo problema è stato risolto mantenendo i flussi ABR in ordine quando le impostazioni ABR vengono fornite con l’impostazione initialBitrate su un flusso che include URL di failover. In questo modo si evita di riprodurre i flussi di failover anziché quelli primari.

* (ZD# 25076) Arresto anomalo di PTAuditudeAdResolver loadComplete

È stato risolto il problema relativo all&#39;arresto anomalo durante l&#39;avvio/arresto rapido di più istanze PTMediaPlayer con annunci.

* (ZD# 25960) Nessun tag sottoscritto aggiuntivo che attiva le trasmissioni delle notifiche di modifica dei metadati

Il problema in cui un tag sottoscritto non viene notificato quando viene visualizzato prima che il primo segmento nel manifesto sia stato risolto.

* (ZD# 26084) PSDK che genera un 106000.101000.-11833 errore decoder non trovato durante la transizione dall’ultima interruzione pubblicitaria al contenuto di intrattenimento

Quando l’ora di inizio dell’ultima interruzione pubblicitaria dalla VMAP cade prima che la durata totale sia stata completata, in determinate condizioni la chiave viene inserita solo dopo la fine dell’ultima interruzione pubblicitaria. Questo problema è stato risolto.

* La Video Heartbeat Library (VHL) è stata aggiornata alla versione 1.5.9 per risolvere i seguenti problemi:

   * (ZD #22351) VHL - Analytics: durata risorsa video live

Questo problema è stato risolto aggiungendo l’API assetDuration a `PTVideoAnalyticsTrackingMetadata` per aggiornare la durata della risorsa per i flussi live/lineari e fornire una logica per il controllo del flusso live.

* (ZD# 22675) VHL - Analytics: aggiornamento della durata delle risorse video live

Questo problema è lo stesso di ZD #22351.

* (ZD #25908) VHL - Analytics: Arresto anomalo di un evento Heartbeat in Adobe

Questo problema è stato risolto aggiornando l’implementazione per utilizzare l’ultima versione di VHL per iOS 1.5.9 al fine di migliorare stabilità e prestazioni.

* (ZD #25956) VHL - Analytics: Arresto anomalo durante la riproduzione ripetuta di video

Questo problema è lo stesso di ZD #25908.

**Versione 1.4.29** (1.4.29,743)

* (ZD# 23901) Gli annunci di terze parti non vengono riprodotti

Questo problema è stato risolto spostandosi sulla struttura URL CRS v3 per includere l’ID di zona nell’URL ricompilato.

* (ZD #25183) Problemi relativi alla riproduzione DRM su tvOS e iOS

Questo problema è stato risolto fornendo supporto per più tag chiave necessari per il supporto di più DRM.

* (ZD# 25334) TVSDK non riesce a riprodurre un contenuto condiviso cDVR

Questo problema è stato risolto impedendo a TVSDK di convertire stringhe vuote in URL assoluti.

* (ZD# 25347) Imposta intestazione HTTP personalizzata su AVURLAsset

È stato aggiunto il supporto per le intestazioni personalizzate nelle richieste dei segmenti tramite la classe PTNetworkConfiguration.

**Versione 1.4.28** (1.4.28.722)

* (ZD #24549) Più chiamate di tracciamento degli annunci

Questo problema è stato risolto aggiornando il gestore della timeline in modo che ascolti le notifiche su un oggetto specifico quando vengono creati più lettori.

* (ZD #24758) PTManifestLogger non supporta iOS 8

Questo problema è stato risolto aggiornando la libreria dell’utilità di registrazione alla versione 7.0 della destinazione di distribuzione.

* (ZD #24775) Flusso ritardato a causa di annunci

Questo problema è stato risolto calcolando correttamente la deviazione della durata nelle playlist degli eventi.

* (ZD #24799) Alcuni episodi non vengono riprodotti nell’APP iOS

Questo problema è stato risolto utilizzando il server web locale per i sottotitoli quando i file WebVTT sono soggetti a restrizioni geografiche.

**Versione 1.4.27** (1.4.27.711) per iOS 6.0+

* (#24089 ZD) - Ottimizzazioni per la risoluzione degli annunci su flussi DVR lunghi

Questo problema è stato risolto aggiungendo più ottimizzazioni per ridurre il tempo necessario per elaborare la finestra DVR in flussi live/lineari.

* (#21554 ZD) - Beacon di errore TVSDK non attivati per tipo di applicazione = video/mp4

Questo problema è stato risolto abilitando il lettore a eseguire il ping degli URL di tracciamento degli errori corretti su formati di risorse non validi.

* (#24424 ZD) - Arresto anomalo di tipo EXC_BAD_ACCESS KERN_INVALID_ADDRESS ha origine dall’interno di PSDKLib per iOS su dispositivi hardware più recenti.

È stato corretto l’arresto anomalo che si verificava a causa di un’istanza del lettore multimediale deallocata, quando la riproduzione veniva scambiata rapidamente tra flussi diversi.

* (#24575 ZD) - Arresto anomalo in TVSDK su dispositivi a 32 bit quando enableDebugLog=true

Il problema nel formato del registro che ha causato l’arresto anomalo su dispositivi a 32 bit quando la registrazione è abilitata è stato risolto.

**Versione 1.4.26** (1.4.26.702) per iOS 6.0+

* (ZD# 20213) - TVSDK FW deve essere dinamico/modularizzato per XCode7

   * Risolto aggiornando le librerie con il supporto dei moduli

**Versione 1.4.25** (1.4.25.684) per iOS 6.0+

* (ZD #19629) - Le pause video live si verificano quando si entra in modalità di riproduzione su ATV 4

Questo problema è stato risolto aggiungendo un periodo di attesa dopo la rimozione dei vecchi elementi, ma prima di aggiungere nuovi elementi ad AVQueuePlayer. Senza il periodo di attesa, le notifiche vengono inviate all&#39;elemento errato.

* (#19856 ZD) - Nessun sottotitolo visualizzato se attivato per impostazione predefinita

I problemi nella playlist webvtt, che impedivano la corretta visualizzazione dei sottotitoli, sono stati risolti.

* (ZD #21590) - Prestazioni video e tracciamento nelle build più recenti

È stato risolto il problema relativo alla lunghezza video mancante in VideoAnalytics.

* (ZD #20202) - L’impostazione dello stile dei sottotitoli personalizzati arresta l’app iOS

Questo problema è stato risolto aggiungendo ulteriori controlli di oggetto nullo durante l’impostazione degli stili dei sottotitoli.

* (#20709 ZD) - lunghezza video riportata come 0 nel tracciamento dell’avvio del video

Questo problema è lo stesso di (#21590 ZD).

* (ZD #22280) - La lunghezza del video di Analytics è impostata su 0

Questo problema è lo stesso di (#21590 ZD).

* (ZD #22592) - Problemi relativi a Airplay in Primetime

Questo problema è lo stesso di (#19629 ZD).

* (ZD#22922) - Commutazione manuale del bitrate per iOS

Questo problema è stato risolto fornendo un’opzione per specificare il bitrate massimo.

* (#23084 ZD) - Conformità Apple per le reti solo IPv6

I simboli non consigliati da Apple per la compatibilità IPv6 sono stati rimossi.

**Versione 1.4.24** (1.4.24.661) per iOS 6.0+

* ZD #2548) - Supporto Primetime per pubblicità interattiva su dispositivi mobili - VPAID 2.0

Questo problema è stato risolto aggiornando la logica per rendere visibile la visualizzazione del lettore se un annuncio VPAID non viene riprodotto.

* (#20101 ZD) - L’implementazione del capitolo personalizzato genera l’evento di inizio del capitolo durante la riproduzione dell’annuncio

Questo problema è stato risolto aggiornando VideoAnalyticsTracker per rilevare correttamente il capitolo iniziale/completo durante la transizione tra i limiti dei capitoli e non dei capitoli.

* (ZD #20784) - Analytics: attivazione della riproduzione dei contenuti completata per le transizioni video live

Questo problema è stato risolto aggiungendo una logica per attivare manualmente il completamento del contenuto durante una sessione di tracciamento video.

Sono state aggiornate le seguenti librerie:

* Libreria AdobeMobile alla versione 4.10.0
* Libreria VHL alla versione 1.5.6
* VHL-Nielsen alla libreria 1.6.7
* (ZD #21855) - I sottotitoli non vengono riprodotti dopo il mid-roll

In questo problema, i tag di discontinuità duplicati causavano la mancata visualizzazione dei sottotitoli dopo il mid-roll. Questo problema è stato risolto rimuovendo i tag di discontinuità adiacenti.

* (#21994 ZD) - Stringa fuori limite nelle sezioni PTHLSU

La causa più probabile dell&#39;arresto anomalo è quando un EXT-X-KEY ha un URL racchiuso tra virgolette.

* ZD #22074) - Arresto anomalo di AUDVAST con frequenza di un minuto su iOS

Nella versione 1.4.23, l’arresto anomalo causato dalla presenza di caratteri non sicuri in un URL di reindirizzamento VAST è stato corretto. Tuttavia, TVSDK continuava a saltare questi annunci.

Questo problema è stato risolto gestendo i caratteri non sicuri e consentendo la riproduzione degli annunci.

* (#22694 ZD) - PTMediaPlayer.  La vista è nascosta dal lettore

Questo problema è stato risolto aggiornando la logica per rendere visibile la visualizzazione del lettore se un annuncio VPAID non viene riprodotto.

**Versione 1.4.23** (1.4.23.641) per iOS 6.0+

* (ZD #18016) - Nessuna risposta dall’SDK Primetime con condizioni di rete non valide

Questo problema è stato risolto migliorando la notifica di errore quando si verifica un errore irreversibile da AVFfoundation e consentendo all&#39;app di gestire il riavvio dopo l&#39;errore.

* (#20580 ZD) - Arresto anomalo in PTSplicerManager

Questo problema è stato risolto fornendo un’ulteriore protezione dai problemi di concorrenza che causano l’arresto anomalo.

* (#21782 ZD) - 10100 codice di errore iOS

È stato risolto il problema a causa del quale TVSDK restituiva un errore 101000 durante l’avvio della riproduzione su flussi DRM di accesso di Adobe.

* (#21889 ZD) - La riproduzione di annunci online e contenuti offline non riesce

Il problema che causava l’errore di riproduzione dopo la risoluzione di un annuncio su contenuto offline crittografato AES.

* (ZD #22074) - Arresto anomalo di AUDVAST ogni minuto su iOS

Questo problema è stato risolto migliorando la gestione dei tag VAST di terze parti che contengono caratteri non validi nell’URL.

* (#22257 ZD) - TVSDK non è in grado di riprodurre il flusso DRM

È stato risolto il problema a causa del quale il TVSDK che restituiva un errore 101000 durante l’avvio della riproduzione su flussi DRM di accesso in Adobe.

**Versione 1.4.22** (1.4.22.627) per iOS 6.0+

* (#18709 ZD) - Arresto anomalo in TVSDK per iOS

È stato risolto il problema relativo a un arresto anomalo che si verificava su alcuni flussi protetti da DRM di accesso di Adobe.

* (#18850 ZD) - Aggiorna la logica di selezione creativa in base alle regole CRS

Questo problema è stato risolto aggiungendo un file di configurazione .json per specificare la priorità della selezione creativa.

* (#19770 ZD) - Il feed video AES protetto non viene più riprodotto

È stato risolto il problema che impediva la riproduzione di alcuni flussi reindirizzati 302.

* (ZD #19629) - Le pause video live si verificano quando si entra in modalità di riproduzione su ATV 4

Questo problema è stato risolto aggiungendo una soluzione alternativa per la pausa video in diretta quando la riproduzione in onda è attivata per i dispositivi Apple TV 4. Il problema sembra essere un problema AppleTV 4.

* (#21119 ZD) - Il TVSDK si arresta dopo la riproduzione dell’annuncio

È stato aggiunto il supporto per i flussi crittografati AES con una sequenza IV durante l’utilizzo dell’inserimento di annunci.

* (ZD #21125) - Ritorno dall’interruzione pubblicitaria live/lineare in anticipo

È stato aggiunto il supporto per il ritorno da un’interruzione pubblicitaria prima che l’interruzione pubblicitaria venga riprodotta fino al completamento. Il ritorno anticipato è indicato tramite un tag manifesto personalizzato.

* (ZD #21224) - Supporto Airplay per flussi tokenizzati da Akamai

Sono state aggiunte API alla classe PTNetworkConfiguration per aggiungere cookie come parametri URL sui segmenti per alcuni flussi tokenizzati Akamai.

* (ZD #21287) - Registro estraneo

È stato risolto un problema con alcune istruzioni di registro visualizzate per impostazione predefinita nella console xcode anche quando la registrazione è disabilitata.

* (#21446 ZD) - Eventi di interruzione annuncio talvolta non attivati da TVSDK

Nei flussi EVENTO, le interruzioni pubblicitarie non vengono attivate correttamente nella build della versione precedente. Questa build risolve questo problema.

**1.4.21** (1.4.21.605) per iOS 6.0+

* (#20749 ZD) - Il fallback ignora le risposte VAST non vuote; gli URL aggiuntivi di tracciamento degli annunci si attivano

È stato risolto un problema relativo ai ping duplicati negli annunci di fallback.

**1.4.20** (1.4.20.590) per iOS 6.0+

* (#18639 ZD) - Il TVSDK utilizza CPU/risorse eccessive su una risorsa di registrazione a caldo di lunga durata

L’utilizzo eccessivo di CPU/risorse è stato corretto nei due livelli. Innanzitutto, consentendo l’esecuzione della funzione di aggiornamento del tempo su una coda globale, invece del thread principale, e ottimizzando l’utilizzo della CPU per l’analisi del manifesto con il file m3u8 elaborato e memorizzato nella cache in precedenza.

* (#19349 ZD) - Gli annunci pre-roll vengono ignorati quando si limita la connessione di rete.

Questo problema è stato risolto fornendo un evento di timeout (requestTimeout) all’applicazione e agli adMetadata.  API adRequestTimeout per ignorare il timeout predefinito di 10 secondi.

* (ZD #19446) - Notifica mancante sui flussi live

Questo problema è stato risolto consentendo all’applicazione di abbonarsi al EXT-X-PROGRAM-DATE-TIME sui flussi in tempo reale.

* (#19459 ZD) - Arresto anomalo durante la preparazione di audio alternativo con PTMediaPlayerItem preparationAudioOptionsWithAVMediaSelectionOptions
* (#19460 ZD) - Arresto anomalo - [PTMediaPlayerItem, preparazioneSottotitoliOpzioniConAVMediaSelectionOptions:nonForcedOptions:]

Questo problema è lo stesso di Zendesk #19459.

* (#19574 ZD) - TVSDK non restituisce i dati di risposta M3U8 per il contenuto DRM o non DRM

Nel caricamento iniziale del file manifesto in PTMediaPlayerItem.preparationToPlay, se il caricamento del manifesto non è riuscito, TVSDK non segnala il corpo della risposta all&#39;errore all&#39;applicazione.

Questo problema è stato risolto consentendo a TVSDK di segnalare la risposta di errore come errore all’applicazione.

* (#19615 ZD) - La logica di fallback non funziona

Nell’implementazione corrente, gli annunci di fallback venivano saltati e non venivano ricompilati a meno che questi annunci non fossero nel formato m3u8. Questo problema è stato risolto aggiungendo anche il supporto per la ricompilazione degli annunci di fallback.

* (#19770 ZD) - TVSDK non riproduce alcun contenuto AES protetto con reindirizzamento 302

Il problema di reindirizzamento è stato risolto perché l’URL di reindirizzamento veniva eliminato da cleanConnectionData prima di poter essere utilizzato per analizzare il manifesto.

* (#19856 ZD) - I sottotitoli non vengono visualizzati per alcune velocità di trasmissione quando sono abilitati per impostazione predefinita

Questo problema è stato risolto gestendo l’errore di iOS per i segmenti dei flussi in cui i sottotitoli non vengono visualizzati.

* (#19868 ZD) - TVSDK si blocca quando viene inviato un contenuto creativo non valido

È stato corretto l’arresto anomalo nel TVSDK che stava deallocando erroneamente un’istanza del vasto parser.

* (#20180 ZD) - Gli annunci VPAID vengono saltati occasionalmente

Il tipo mime JavaScript non veniva sempre incluso o considerato come un tipo mime valido. Questo problema è stato risolto includendo JavaScript come tipo mime valido.

* (#20749 ZD) - Il fallback ignora le risposte VAST non vuote; gli URL aggiuntivi di tracciamento degli annunci si attivano

È stato risolto il problema che impediva il riconfezionamento di alcuni dei creativi.

**Versione 1.4.19** (1.4.19.563) per iOS 6.0+

* ZD #18639) - Il TVSDK utilizza una quantità eccessiva di CPU/risorse su una risorsa di registrazione a caldo

Questo problema è stato risolto ottimizzando la riscrittura della playlist DRM m m3u8 sui bit della cache della playlist che sono stati precedentemente riscritti. Questo è più rilevante quando si riproducono flussi live m3u8 per i quali m3u8 viene scaricato dopo ogni download di segmenti.

* (ZD#18956) - player.drmManager è nullo quando il punto di interruzione è impostato in iOS Demo Player

Questo problema è stato risolto aggiornando l’implementazione dell’API PTMediaPlayer.drmManager per raccogliere DRManager dal framework DRM.

**Versione 1.4.18** ( 1.4.18.557) per iOS 6.0+

* (ZD #18844) Testina di riproduzione per il tracciamento dei contenuti live nel lettore iOS.

Questo problema è stato risolto consentendo alle applicazioni di impostare il proprio valore di testina di riproduzione.

* #18518 Zendesk - Se il nome del video non è specificato, il nome predefinito del TVSDK è *Lettore basato su PSDK.*

Questo problema è stato risolto rimuovendo il valore predefinito per il nome del lettore.

**Versione 1.4.17** (1.4.17.545) per iOS 6.0+

* Zendesk #2228 - Migliora il TVSDK per restituire la risposta JSON del recupero di un manifesto

Invece di inviare un errore quando il contenuto non è M3U8, DRM Framework restituisce un valore DRMMetadata nil. Il problema è stato risolto aggiungendo metadati per esporre il contenuto quando si verifica la notifica M3U8_PARSER_ERROR.

* #2231 Zendesk - Errore restituito dal recupero del manifesto non disponibile in MediaPlayerNotification

Stessa risoluzione di Zendesk #2228

* #3304 Zendesk - VAST 3.0 `[ERRORCODE]` la macro non viene compilata

È stato risolto il problema per cui l’SDK di Auditude non riesce a inviare un ping se l’URL di tracciamento contiene spazi all’inizio.

* #17294 Zendesk - Arresto anomalo SecKeyRawSign

È stato risolto un possibile arresto anomalo quando il codice del cliente utilizza la catena di chiavi.

* Zendesk #18008 - Supporto dei cookie per iOS8+ per supportare i flussi tokenizzati

I flussi tokenizzati di Akamai richiedono l’invio di cookie per le richieste dei segmenti, e questo non era possibile in iOS 7 e versioni precedenti. A partire da iOS 8, Apple ha aggiunto un’API che consente di trasmettere i cookie per le richieste dei segmenti. Questo supporto è ora disponibile in TVSDK . È stato aggiunto anche il supporto per l’invio di un agente utente, se disponibile.

* Zendesk #18166 - TVSDK 1.4.15 fornisce centinaia di avvisi durante la compilazione con DWARF con le opzioni di file dSYM

Tutti gli avvisi sono stati risolti.

**Nota**: sono state aggiunte librerie compatibili con tvOS per TVSDK.

**Versione 1.4.16** (1.4.16.1454)

* Zendesk #3875 - La scheda S si blocca durante la riproduzione

Ripristino della dipendenza di OKHTTP dall’audit per CRS in quanto TVSDK utilizza ora direttamente httpurlconnection anziché curl. Il problema è stato risolto cancellando le eccezioni prima di effettuare un’altra chiamata JNI.

* Zendesk #4487 - Tracciamento del canale lineare dei contenuti

Il problema è stato risolto inizializzando nuovamente il tracciatore heartbeat video durante una sessione di riproduzione con flusso lineare.

* Zendesk #17919 - Android - la ricerca dei contenuti causa un errore heartbeat

Il problema era risolvere l’heartbeat in uno stato di errore quando si verifica una ricerca in un capitolo

* Zendesk #18053 - L’applicazione che utilizza TVSDK si blocca su Marshmallow

Il TVSDK si bloccava sul sistema operativo Android M quando la libreria TVSDK utilizzava un codice al neon che eseguiva la conversione del colore YUV -> RGB. Questo problema è stato risolto aggiornando le funzioni che causano il problema utilizzando una versione non neon del codice .

* Zendesk #18072 - Android M - Arresto anomalo dell’applicazione

Questo arresto anomalo si verifica durante la chiamata delle API MediaCodecList e MediaCodecInfo durante il controllo del supporto del profilo e del livello. Adobe sta cercando il supporto di Google per ulteriori informazioni. Questo problema è stato risolto fornendo un lavoro temporaneo caricando in anticipo tutte le informazioni del codec per evitare di chiamare queste API solo quando sono necessarie informazioni del codec.

* Zendesk #18074 - I sottotitoli in arabo non funzionano su Nexus con Android 6.0

Questo problema è stato risolto fornendo supporto per la mappa font Android CTS.

**Versione 1.4.15** (1.4.15.512) per iOS 6.0+

**Nota**: il modulo Nielsen è stato rimosso dalla build TVSDK, ma TVSDK verrà aggiornato nel prossimo futuro con un nuovo modulo di integrazione Nielsen.

* (#2228 ZD) - Errore restituito dal recupero del manifesto non disponibile in MediaPlayerNotification

Sono stati aggiunti metadati per esporre il contenuto quando si verifica la notifica M3U8_PARSER_ERROR.

* (#4437 ZD) - Arresti anomali all’interno dell’SDK di Adobe Primetime

È stato corretto un arresto anomalo che si verificava durante la preparazione di sottotitoli/audio alternativo.

* (ZD #4487) - Tracciamento del canale lineare del contenuto

È consentita la reinizializzazione del tracciamento heartbeat video durante una sessione di riproduzione con flusso lineare.

**Versione 1.4.14** (1.4.14.498) per iOS 6.0+

* (#17260 ZD) - Arresto anomalo di playlistManagerForURL

È stato corretto un arresto anomalo intermittente a causa di problemi di concorrenza.

**Versione 1.4.13** (iOS 6.0+)

* (#3304 ZD) - VAST 3.0 `[ERRORCODE]` la macro non viene compilata

   * Se l’annuncio in linea non è creativo, viene visualizzato il codice di errore 400.
   * `[ERRORCODE]` La macro verrà codificata in URL.

* (ZD #3865) Integrazione Heartbeat con annunci IMA

È stato corretto un bug a causa del quale la lunghezza del video veniva segnalata in modo errato.

* Aggiornamento del lettore demo TVSDK per supportare iOS 9

Per supportare correttamente iOS 9, è necessario configurare le eccezioni della sicurezza trasporto applicazioni. Ai fini della demo, l&#39;ATS è completamente disabilitato.

**Versione 1.4.12** (1.4.12.464) per iOS 6.0+

* (ZD #4521) Test CRS lato client e SSAI

È stato corretto l’errore inverso MD5 nell’URL 3P.

**Versione 1.4.12** (1.4.12.463) per iOS 6.0+

* (ZD #2751) CSAI e CRS | Miglioramento: gestisci gli elementi dinamici in determinati URL di file multimediali.

È stato aggiornato il servizio Creative Repackaging per gestire correttamente gli annunci con URL creativi dinamici.

* (ZD #3654) Perdita di memoria nella versione PSDK dopo 1.3.4.166

Perdita di memoria fissa in drmFramework con riproduzione regolare su dispositivi iOS 8.2

* (ZD #3988) Il preroll viene saltato quando si cerca di nuovo in esso dopo la prima riproduzione

È stato corretto un bug che impediva la corretta disattivazione dei criteri di annuncio.

* (ZD #4017) Richiesta dell’API di iOS per forzare la riproduzione di un annuncio su ricerca all’indietro

Risolto con correzione per #4279 ZD

* (ZD #4279) Problema di reindirizzamento ad insertion -302 di HLS TVSDK su iOS e desktop

È stato corretto un bug a causa del quale una risorsa annuncio utilizzava un URL di reindirizzamento relativo

**Versione 1.4.9** (1.4.9.427) per iOS 6.0+

* (ZD #3075) Problema di raggiungibilità Internet - iOS

È stata aggiunta una notifica per rilevare quando la riproduzione si è arrestata.

* (ZD #3193) Richiesta di API per la modifica del profilo in TVSDK

È stato aggiornato PTPlaybackInformation per esporre l’indicatoreBitrate indicato aggiornato. È stata aggiornata la notifica BITRATE_CHANGE per essere più affidabile in termini di tempo e accurata rispetto ai bitrate riportati da M3U8.

* (ZD #3324) Problema di segnalazione degli annunci Primetime quando non sono presenti annunci multimediali in VMAP

Supporto per il ping di URL di tracciamento delle interruzioni pubblicitarie vuoti, TVSDK verificherà ora i ping di avvio e completamento delle interruzioni pubblicitarie vuote

**Versione 1.4.8** (1.4.8.402)

* (#3158 ZD) Arresto anomalo di IOS 7 durante la riproduzione completa degli eventi

**Versione 1.4.7** (1.4.7.382)

* (ZD #2197) Tracciamento degli errori pubblicitari. La notifica aggiunta per la risorsa non è riuscita a caricare il manifesto.
* (ZD #2894) Il lettore effettua 4 richieste manifest di livello superiore durante la riproduzione.
* (ZD #2992) Auditude di segnalazione di durate e identificatori strani.

**Versione 1.4.6**(1.4.6.325)

* (ZD #2197) Tracciamento degli errori pubblicitari. La notifica aggiunta per la risorsa non è riuscita a caricare il manifesto

**Versione 1.4.5** (1.4.5.283)

* (ZD #2141) Implementazione di Analytics per l&#39;app TreeHouse, aggiunta la libreria AdobeAnalyticsPlugin.a per creare il pacchetto.
* Aggiornamento della libreria Video Heartbeat alla versione 1.4.1.2
* (PTPALY-4226) (relativo a ZD #2423) L&#39;esecuzione della reimpostazione DRM può comportare l&#39;eliminazione dei dati del documento dell&#39;applicazione.

**Versione 1.4.4** (1.4.4.242)

* Aggiornamento Video Heartbeats Library (VHL) alla versione 1.4.1.

* (ZD #2435) È necessario aggiornare la documentazione TV SDK relativa alle esigenze di analisi

**Versione 1.4.2** (1.4.2.210: iOS 6.0+)

* (#1129 ZD) _player.currentItem.audioOptions che restituisce vuoto
* (ZD #2109) Primetime PSDK 1.4.1.125 non funziona con Xcode 5.1.1
* (ZD #2137) Arresto anomalo in PSDK su iOS quando non è possibile caricare i metadati DRM

**Versione 1.4.1** (1.4.1.125)

* (ZD #1107) Simboli duplicati CocoaLumberjack
* (ZD #1644) Modificare l’agente utente di iOS per targeting e reporting
* (ZD #1850) File Lumberjack di cacao inclusi nell’SDK di iOS
* (ZD#1908) I tag personalizzati vengono ignorati da PSDK se sono presenti più di 1

**Versione 1.4.0** (1.4.0.32)

* #1024 Zendesk - Funzione per rimuovere un annuncio dal flusso tramite manifesto

## Problemi noti in 1.4 {#known-issues-in}

* In iOS TVSDK , tutti gli annunci sono uniti nel manifesto del contenuto. I comportamenti di annuncio vengono implementati effettuando ricerche in base alla durata del contenuto e dei segmenti di annuncio. Pertanto, se le durate dei segmenti non sono precise, la ricerca potrebbe non terminare sempre al fotogramma esatto dell’inizio o della fine dell’interruzione pubblicitaria. Anche se le durate sono per il fotogramma, c&#39;è una tolleranza che la piattaforma stessa impone sulla ricerca e ci possono essere alcuni fotogrammi o annunci o contenuti visualizzati. Si tratta di una limitazione della piattaforma e del modo in cui l’inserimento di annunci funziona con TVSDK su iOS.
* In questo caso, la decisione di saltare avviene sull’evento di ricerca. Tuttavia, poiché le durate dei segmenti dell’annuncio nel manifesto non rappresentano con precisione la durata effettiva dell’annuncio, la ricerca non è accurata dal frame. Quindi, puoi vedere alcuni fotogrammi dell’annuncio quando vengono applicati i criteri dell’annuncio.
* RECORDING_ERROR: si è verificato un errore durante la registrazione dello schermo.
* Potrebbe verificarsi che il video di rotazione della licenza non venga riprodotto su iOS 11 e che venga riprodotto correttamente su iOS 9.x e iOS 10.x.
* Nel supporto VPAID 2.0, se la riproduzione è attiva su AirPlay, gli annunci VPAID vengono saltati.
* Il file drmNativeInterface.framework non viene collegato correttamente se la destinazione minima è impostata su iOS7 (o versione successiva).\
  Soluzione alternativa: specifica esplicitamente la `libstdc++6`.  libreria dylib come segue: Vai a Target->Fasi build->Collega binario a librerie e aggiungi `libstdc++.6.dylib`.

* L’annuncio post-roll non viene inserito per la sostituzione dell’API.
* La ricerca in un’interruzione pubblicitaria (senza uscirne) genera un annuncio duplicato e avvia una notifica di interruzione pubblicitaria
* L&#39;impostazione currentTimeUpdateInterval non ha alcun effetto.\
  Nota: in alcune versioni di iOS, il sistema operativo non carica automaticamente le risorse all&#39;interno di PSDKLibrary.framework. È importante copiare manualmente il file PSDKResources.bundle nelle risorse bundle dell’applicazione: vai a &quot;Fasi build&quot; e copia le risorse bundle.
* Non è possibile creare l’app di riferimento con Xcode 8 o versioni precedenti. iOS TVSDK versione 1.4.41 e successive, utilizza Xcode 9 per la compilazione.

## Risorse utili {#helpful-resources}

* Consulta la documentazione completa dell’Aiuto all’indirizzo [Informazioni e supporto per Adobe Primetime](https://helpx.adobe.com/support/primetime.html) pagina.
