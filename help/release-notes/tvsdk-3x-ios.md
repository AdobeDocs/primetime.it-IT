---
title: Note sulla versione TVSDK 3.11 per iOS
description: TVSDK 3.11 per iOS - Note sulla versione - descrive le novità o le modifiche apportate, i problemi risolti e noti e i problemi del dispositivo in TVSDK iOS 3.11.
translation-type: tm+mt
source-git-commit: ac75f63f98060e1937570476362bb5d4458d1f85

---


# Note sulla versione TVSDK 3.11 per iOS {#tvsdk-for-ios-release-notes}

TVSDK 3.11 per iOS - Note sulla versione - descrive le novità o le modifiche apportate, i problemi risolti e noti e i problemi del dispositivo in TVSDK iOS 3.11.

## Requisiti di sistema e software {#system-software-requirements}

Prima di scaricare iOS 3.11, assicurati che le versioni di hardware, sistemi operativi e applicazioni siano conformi ai seguenti requisiti:

Sistema operativo: iOS 8.0 o versione successiva.

## iOS TVSDK 3.11

Correzioni dei problemi dei clienti per i quali `isFallbackOnInvalidCreativeEnabled` e i metodi `customParams` causano l&#39;arresto anomalo dell&#39;applicazione.

Per le correzioni nella versione corrente, consultate la sezione sui problemi [dei clienti risolti](#resolved-issues) e, per le limitazioni, consultate la sezione sui problemi e sulle limitazioni [noti](#known-issues-and-limitations) .

### Nuove funzioni e problemi risolti nelle versioni precedenti {#whats-new-previous}

**iOS TVSDK 3.10**

* È stato risolto un problema per il quale il lettore TVSDK non attivava `PTMediaPlayerStatusError` le notifiche quando la rete non era disponibile.

**iOS TVSDK 3.9**

* È stato corretto un problema a causa del quale i sottotitoli VTT non riuscivano a riprodursi causando il blocco dell&#39;app.

* iOS TVSDK 3.9 include il certificato di trasporto di individualizzazione aggiornato.

**Hotfix per iOS TVSDK 3.8.0.83**

L&#39;hotfix dispone del certificato di trasporto di individualizzazione aggiornato.

**iOS TVSDK 3.8**

Conformità con iOS 13 e gestione obsoleta dell&#39;API UIWebView di iOS 13.

**iOS TVSDK 3.7**

Hotfix per uno scenario in cui la riproduzione si arresta quando un numero elevato di richieste di risoluzione di annunci veniva effettuato contemporaneamente.

**iOS TVSDK 3.6**

**Correzioni nella proprietà wideXML della classe`PTNetworkAdInfo`**

La proprietà wideXML non veniva impostata correttamente e restituiva un valore nil.

**iOS TVSDK 3.5**

**Abilitazione dell&#39;audio sullo sfondo**

*Configurate l&#39;app per continuare a riprodurre l&#39;audio quando entra in background.*

Per abilitare questa funzione, è necessario impostare la nuova API `audioPlaybackInBackground` aggiunta nella classe PTMediaPlayer. Con questa API abilitata, l&#39;app è pronta per riprodurre l&#39;audio in background.

**iOS TVSDK 3.4.0.19 (Hotfix)**

Questa release contiene una correzione per gli arresti anomali dell&#39;applicazione che si verificano in uno scenario di failover degli annunci.

**iOS TVSDK 3.4**

**Timeout risoluzione annuncio**

* Con TVSDK 3.4, gli utenti ora possono impostare il valore di timeout per la risoluzione complessiva degli annunci e i download del manifesto. Se entro un determinato timeout alcuni annunci non vengono risolti, TVSDK riprodurrà gli annunci rimanenti.

* PTAdMetadata: l&#39;API adRequestTimeout è obsoleta e verrà rimossa. Il valore predefinito è stato impostato su 35 secondi.

* Nel PTAdMetadataClass sono state introdotte due nuove API alternative: adResolutionTimeout - timeout per le chiamate adManifestTimeout complessive per la risoluzione degli annunci - timeout per i download del manifesto degli annunci.

**Ottimizzazione delle entrate**

TVSDK abilitato per identificare le aree problematiche correlate ai flussi di lavoro di inserimento annunci per eseguire il report a un punto finale di scelta dell&#39;analisi.

**Versione 3.3**

TVSDK 3.3 è ora compatibile con l&#39;SDK iOS 11. Tutte le API obsolete sono state sostituite con alternative adeguate.

**Versione 3.2**

**Ulteriore supporto per la registrazione (fase 2)**

È stato aggiunto il supporto per le notifiche di errore, in caso di:

* La versione HLS dell&#39;annuncio utilizza un livello più alto del contenuto.

* È esclusa la variante solo audio.

* Richiesta VAST/VMAP non riuscita.

**Versione 3.1**

* **Supporto** aggiuntivo per la registrazione È stato aggiunto il supporto per le notifiche descrittive in caso di problemi di riproduzione degli annunci.

* **È stato aggiunto il supporto** di flussi CMAF crittografati Fairplay con riproduzione di codec AVC.

**Versione 3.0.1**

Nessuna nuova funzione o miglioramenti in questa versione.

**Versione 3.0**

* TVSDK 3.0 supporta flussi HEVC.

* Just In Time - Risoluzione di annunci più vicini agli indicatori di annunci.

Aggiunta `enableDelayAdLoading` proprietà di tipo booleano nell&#39;interfaccia a livello di app per abilitare JIT. Se `enableDelayAdLoading` è NO, verrà `setadMetadata.delayAdLoading`impostato su True (proprietà dell&#39;interfaccia PTAdMetadata).

Con questa proprietà abilitata, TVSDK risolve ogni interruzione di annuncio prima della sua posizione in base al valore di tolleranza definito. Per impostazione predefinita, `delayAdTolerance` è impostato su 5 secondi.

**Versione 1.4.45**

Per conformarsi a Xcode10, TVSDK è stato spostato da &quot;`libstdc++`&quot; a &quot;`libc++`&quot; e di conseguenza la versione minima supportata è iOS 7. Precedentemente era iOS 6.

**Versione 1.4.44**

Nessuna nuova funzione o miglioramenti in questa versione.

**Versione 1.4.43**

* Esperienza simile a quella televisiva, grazie alla quale è possibile partecipare al mezzo di un annuncio senza attivare il tracciamento parziale degli annunci.\
   Esempio: L&#39;utente si unisce al centro (a 40 secondi) di un annuncio pubblicitario di 90 secondi composto da tre annunci da 30 secondi. Questo è 10 secondi dopo il secondo annuncio nell&#39;interruzione.

   * Il secondo annuncio viene riprodotto per la durata rimanente (20 sec) seguita dal terzo annuncio.
   * I tracciatori di annunci per l&#39;annuncio parziale riprodotto (secondo annuncio) non vengono attivati. Vengono attivati solo i tracciatori del terzo annuncio.

* È stata aggiunta la proprietà enableVodPreroll di tipo booleano nell&#39;interfaccia PTAdMetadata. La proprietà può essere utilizzata per abilitare il pre-roll su un flusso VoD. Se enableVodPreroll è NO, PSDK non viene riprodotto pre-roll. Questo, tuttavia, non ha alcun impatto sui midroli. Il valore predefinito di enableVodPreroll è YES.
* closedCaptionDisplayEnabled API dell’interfaccia PTMediaPlayer è contrassegnata come obsoleta a partire da iOS v1.4.43. Per determinare se sono disponibili sottotitoli codificati per un dato PTMediaPlayerItem, esaminare la proprietà subtitleOptions di PTMediaPlayerMediaItem.

**Versione 1.4.42**

In questa versione non vengono aggiunte nuove funzioni. Per un elenco dei problemi risolti, consultate [Problemi](#resolved-issues)risolti.

**Versione 1.4.41**

Modifiche API:

* **isSecure**: È stata introdotta una nuova API isSecure per impedire al lettore di registrare e generare un errore. Il valore predefinito è true.

* **allowExternalRecording**: È stata introdotta una nuova API per consentire il mirroring della riproduzione aerea per un contenuto protetto. Il mirroring dell&#39;airplay viene trattato come registrazione, pertanto `allowExternalRecording` il valore deve essere impostato su `True`, per consentire il mirroring dell&#39;airplay o impostato `False` per arrestare il mirroring dell&#39;airplay per il contenuto protetto. Per impostazione predefinita, `value` è true.

**Versione 1.4.40**

Nessuna nuova funzionalità.

**Versione 1.4.39**

* IOS TVSDK è certificato con VHL 2.0.1 e con VHL 2.0.1 con Nielsen.

* L&#39;SDK per iOS TVSDK viene aggiornato per effettuare richieste CRS dal nuovo host Akamai `primetime-a.akamaihd.net`.

* La nuova configurazione del nome host consente la distribuzione delle risorse CRS sia tramite HTTP che HTTPS (SSL) su scala maggiore.

**Versione 1.4.36**

Integrare e certificare VHL 2.0 in iOS TVSDK: Ridurre la barriera nell&#39; `VideoHeartbeatsLibrary` implementazione riducendo la complessità delle API.

**Versione 1.4.34**

**Informazioni annuncio di rete**

Le API TVSDK ora forniscono informazioni aggiuntive sulle risposte VAST di terze parti. Ad ID, Ad System e VAST Ad Extensions sono forniti in `PTNetworkAdInfo` classe accessibili tramite `networkAdInfo` la proprietà su una Ad Asset. Queste informazioni possono essere utilizzate per l&#39;integrazione con altre piattaforme di Ad Analytics come **Moat Analytics**.

**Versione 1.4.31**

* **Metriche** di fatturazione Per soddisfare i clienti che desiderano pagare solo per ciò che utilizzano, anziché un tasso fisso indipendentemente dall&#39;uso effettivo, Adobe raccoglie le metriche di utilizzo e utilizza queste metriche per determinare quanto addebitare ai clienti.

   Ogni volta che TVSDK genera un evento di avvio del flusso, il lettore inizia a inviare periodicamente messaggi HTTP al sistema di fatturazione di Adobe. Il periodo, noto come durata fatturabile, può essere diverso per VOD standard, pro VOD (annunci mid-roll abilitati) e contenuti live. La durata predefinita di ciascun tipo di contenuto è di 30 minuti, ma il contratto con Adobe determina i valori effettivi.

* **Supporto multi-CDN per CDN Ads** TVSDK ora supporta Multi-CDN per annunci CRS. Fornendo i dettagli FTP per gli annunci CRS, potete specificare posizioni CDN diverse da quelle predefinite della CDN di proprietà di Adobe, ad esempio Akamai.

**Versione 1.4.29**

Nella `PTSDKConfig` classe è stata aggiunta l&#39;API forceHTTPS.

La `PTSDKConfig` classe fornisce metodi per applicare SSL alle richieste effettuate ai server Adobe Primetime ad alsgerment, DRM e Video Analytics. Per ulteriori informazioni, vedere `forceHTTPS` e `isForcingHTTPS` metodi in questa classe. Se un manifesto viene caricato su HTTPS, TVSDK mantiene l&#39;uso del contenuto HTTPS e lo rispetta quando carica eventuali URL relativi da tale manifesto.

>[!NOTE] Le richieste ai domini di terze parti come Pixel di tracciamento annunci, URL di contenuti e annunci e richieste simili non vengono modificate, ed è responsabilità dei provider di contenuto e dei server di annunci fornire URL supportati tramite HTTPS.

**Versione 1.4.18**

Primetime iOS TVSDK ora supporta i creativi JavaScript VPAID 2.0 per consentire un&#39;esperienza pubblicitaria interattiva avanzata. Per ulteriori informazioni su VPAID 2.0, consulta Supporto per annunci VPAID.

**Versione 1.4.17**

* tvOS

   TVSDK supporta le applicazioni native tvOS.
* È possibile riprodurre i seguenti tipi di contenuto:

   * VOD
   * Live
   * AES-128
   * Audio e sottotitoli alternativi
   * FER

* È possibile visualizzare i seguenti tipi di annunci:

   * Base
   * VAST2
   * VAST3
   * VMA

* Le seguenti funzionalità non sono attualmente supportate:

   * Digital Rights Management (DRM)
   * Banner pubblicitari
   * TV Markup Language (TVML)

**Versione 1.4.13**

>[!NOTE] Il modulo Nielsen è stato rimosso dalla build TVSDK. TVSDK verrà aggiornato prossimamente con un nuovo modulo di integrazione Nielsen.

**Ad Fallback, catena a margherita nella logica di selezione degli annunci (Zendesk #3103)**

Per gli annunci VAST (creativi) con la regola di fallback abilitata, TVSDK tratta un annuncio con un tipo MIME non valido come un annuncio vuoto e tenta di utilizzare gli annunci di fallback al suo posto. Potete configurare alcuni aspetti del comportamento di fallback. Per ulteriori informazioni, vedi Abbandono annunci per annunci VAST e VMAP.

**Versione 1.4.9**

**Segnalazione Del Blackout Con Sostituzione Alternativa Dei Contenuti**

Come parte dell&#39;aggiornamento 1.4 TVSDK, ora siamo anche in grado di entrare e tornare dai blackout regionali rispetto ai contenuti lineari. Il TVSDK ora può elaborare due file manifest in parallelo, principale e alternativo, per monitorare i segnali blackout anche quando la programmazione alternativa viene mostrata al posto della programmazione originale.

**Versione 1.4.8**

**Video Heartbeats Library (VHL) aggiornato alla versione 1.5**

* Possibilità di inviare i metadati con l&#39;avvio del video e/o con l&#39;avvio di video/annunci/capitoli come dati contestuali.

* Minore traffico di rete - I battiti di calore sono minori in media e di dimensioni inferiori.

**Versione 1.4.7**

* **Supporto per l&#39;individuazione locale**

Supporto per le installazioni locali di Adobe Individualization Server per personalizzare la richiesta di individualizzazione del client per passare a un endpoint diverso.

* **Protezione dell&#39;uscita basata sulla risoluzione**

I criteri DRM ora possono specificare la risoluzione massima consentita, a seconda delle capacità di protezione dell&#39;output del dispositivo. Ad esempio, &quot;Se è disponibile l&#39;HDCP, è possibile riprodurre contenuti con una risoluzione fino a 1080p e, se l&#39;HDCP non è disponibile, riprodurre contenuti con una risoluzione fino a 480p&quot;.

**Versione 1.4.4**

* **Video Heartbeats Library (VHL) aggiornamento alla versione 1.4.1.1**

   * Aggiunta la possibilità di raggruppare diversi casi di utilizzo di analisi, da altri SDK o lettori, con Adobe Analytics Video Essentials.
   * Il tracciamento degli annunci è stato ottimizzato rimuovendo i `trackAdBreakStart` metodi e `trackAdBreakComplete` . L’interruzione dell’annuncio viene ricavata dalle chiamate `trackAdStart` e ai `trackAdComplete` metodi.
   * La `playhead` proprietà non è più necessaria per il tracciamento degli annunci.
   * È stato aggiunto il supporto per l’ID visitatore di Marketing Cloud.

* **Integrazione SDK Nielsen**

TVSDK ora supporta l’invio di beacon mTVR e MDPR ID3 all’SDK Nielsen senza alcuna integrazione personalizzata. Per iniziare, scarica l’SDK per app iOS 3.1.2.19 Nielsen e segui le istruzioni riportate nella guida ai programmatori iOS.

**Versione 1.4.0**

* **Segnalazione Del Blackout Con Sostituzione Alternativa Dei Contenuti**

Come parte dell’aggiornamento 1.4 TVSDK, TVSDK ora supporta anche l’accesso e il ritorno dai blackout regionali rispetto ai contenuti lineari. Il TVSDK ora può elaborare due file manifest in parallelo, principale e alternativo, per monitorare i segnali blackout anche quando la programmazione alternativa viene mostrata al posto della programmazione originale.

* **Rimuovi/Sostituisci annunci C3**

Ora, non è necessario alcun lavoro di preparazione aggiuntivo per inserire dinamicamente nuovi annunci nelle risorse video-on-demand (VOD) che escono dalla finestra C3. TVSDK fornisce ora un&#39;API per rimuovere intervalli di contenuto personalizzati e inserire nuovi annunci in modo dinamico. Questa nuova potente funzionalità è utile anche nei casi in cui i contenuti live/lineari vengono inviati in onda durante la trasmissione e immediatamente ridotti per essere utilizzati come contenuti on demand senza il tempo necessario per &quot;pulire&quot; la risorsa.

## Problemi risolti {#resolved-issues}

Quando la risoluzione è associata a un problema segnalato, viene visualizzato un riferimento Zendesk, ad esempio ZD#xxxxx.

<!-- 

Comment Type: draft

<note type="note"> 
 <p>All TVSDK customers who use CRS are strongly encouraged to upgrade to TVSDK 1.4.39 or latest on iOS and Android. This upgrade is a drop-in replacement to the existing app implementation. After the upgrade, check for the CRS creative URL requests in a proxy tool (for example, Charles) to verify that the version in the path reflects version 3.1. For example:</p> 
 <p><span class="code">https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/ 167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784bf3586d.m3u8</span></p> 
</note>

 -->

<!--
Comment Type: draft

<note type="note"> 
 <p>TVSDK versions earlier than version 1.4.28 sometimes exhibit a long delay in the startup time when ad-enabled content is played on devices that are running on iOS 10. To resolve this issue, upgrade to version 1.4.28 or later. Version 1.4.28 was released on August 31, 2016, and iOS 10 was released on September 13, 2016.</p> 
</note>
 -->

**iOS TVSDK 3.11**

* (ZD#40998) - Le `isFallbackOnInvalidCreativeEnabled` cause dell&#39;arresto anomalo dell&#39;applicazione.

* (ZD#41289) - `NSInvalidArgumentException` viene osservato con il metodo che `customParams` porta all&#39;arresto anomalo dell&#39;applicazione.

### Risolti i problemi nelle versioni precedenti {#resolved-issues-previous}

**iOS TVSDK 3.10**

(ZD#40943) - Il lettore TVSDK non attiva la notifica PTMediaPlayerStatusError quando la rete non è disponibile.

**iOS TVSDK 3.9**

(ZD#40272) - IOS TVSDK non riproduce i sottotitoli VTT con errore 101001 e porta al blocco dell&#39;app.

**iOS TVSDK 3.8**

* (ZD#40087) - Arresti anomali in iOS con errore del lettore per il contenuto VOD scaduto.

* (ZD#40083) - Gli annunci pre-roll non vengono riprodotti per livestream con `OpportunityGenerator` e il lettore restituisce un errore.

* (ZD#39828) - `CurrentItem` la proprietà manca dell&#39;annotazione di nullità, causando un arresto anomalo del lettore quando lo stato del lettore contenuto nella notifica è `PTMediaPlayerStatusStopped`.

**iOS TVSDK 3.7**

(ZD#38961) - Il contenuto non viene riprodotto nella finestra Picture-in-Picture (PiP) dopo che un contenuto ha completato la riproduzione, quando più contenuti sono configurati per essere riprodotti nel PiP.

**iOS TVSDK 3.6**

Nessun nuovo problema in questa versione.

**iOS TVSDK 3.5**

Nessun nuovo problema in questa versione.

**Versione 3.3**

(ZD#37820): aggiunta della whitelist per l&#39;intestazione personalizzata HS-Id, HS-SSAI-TAG.

**Versione 3.2**

* **Ticket#36588** - Si verifica un arresto anomalo del lettore quando viene chiamato il metodo STOP di MediaPlayer.
È stato corretto un arresto anomalo intermittente che si verificava quando il metodo STOP veniva chiamato per alcuni flussi con sottotitoli.

* **Ticket#37080** - Richieste duplicate visualizzate per chiamate Manifest.
Sono state corrette le richieste duplicate per gli URL Manifest durante la riproduzione. TVSDK effettua ora una chiamata per manifesto.

* **Ticket#37** - La regola di normalizzazione CRS non riesce con il tipo di corrispondenza eqÈ stato corretto un caso in cui si verificava l&#39;arresto anomalo del lettore durante l&#39;utilizzo dell&#39;ultima regola di normalizzazione impostata per i nomi host con il tipo di corrispondenza &quot;eq&quot;.

**Versione 3.1**

**Biglietto #36313** - Risultati intermittenti imprevedibili durante le interruzioni pubblicitarie lineariRiproduzione intermittente corretta durante le interruzioni pubblicitarie lineari nel flusso live.

**Versione 3.0.1**

**Ticket36948** - CRS - Ordine di selezione delle risorse incoerente su iOS 12La risorsa selezionata per CRS non è sempre la variante di qualità più elevata restituita in una risposta VAST o VMAP.

**Versione 3.0**

* **Ticket35311** - Lo stato del lettore non viene PAUSED durante un&#39;interruzione di una chiamata telefonicaAggiunto gestore di interrupt per impedire l&#39;interruzione del lettore. Al momento dell&#39;interruzione, lo stato del lettore diventa PAUSED e quindi riprende la riproduzione facendo clic sul pulsante di riproduzione.

* **Ticket36685** - Risorse dal vivo - Mancata corrispondenza di tempo con l’avanzamento del lettore e il tempo del marcatore SCTEIl tempo corretto è calcolato per i marcatori SCTE che sono in anticipo rispetto al punto attivo.

* **Ticket36492** - `currentTime` e `localTime` non vengono aggiornati quando si cerca di trovare una nuova posizione durante lo stato in pausa. Ora è possibile impostare su zero se il lettore è in stato di pausa; in precedenza, l&#39;ora corrente era impostata su zero solo nello stato di riproduzione.

**Versione 1.4.45**

* **Ticket36294** - iOS TVSDK non funziona con Xcode 10Sono stati corretti i problemi di compilazione con TVSDK su XCode 10. A causa dei requisiti XCode 10, le app create su TVSDK per iOS 1.4.45 in avanti richiedono la destinazione di distribuzione minima come iOS 7.0

* **Ticket36321** - Discrepanza osservata nell&#39;intervallo ricercabile tra `PTMediaPlayer` e `AVPlayer` l&#39;istanza in stato &quot;Playing&quot;.

* **Ticket36493** - `libstdc++` supporto su iOS 12Sono stati risolti i problemi di compilazione con TVSDK su iOS 12. Le app create su TVSDK per iOS 1.4.45 a partire richiedono la destinazione di distribuzione minima come iOS 7.0

**Versione 1.4.44**

* **Ticket34683** - Il Tempo Di Avanzamento Della Riproduzione Degli Annunci Va In Modo Negativo

Controlli aggiuntivi per gestire il caso in cui si verificasse una mancata corrispondenza tra la durata indicata dal server degli annunci e il contenuto effettivo degli annunci.

* **Ticket34801** - currentTime e localTime non venivano aggiornati quando si cercava una nuova posizione durante la pausa statusPlayer&#39;s current time ora può essere impostato su zero se il lettore è in stato di pausa; in precedenza, l&#39;ora corrente era impostata su zero solo nello stato di riproduzione.

* **Ticket35037** - La riproduzione si blocca con un URL errato quando si torna dall&#39;inserimento di annunci basati su segnali.
Correzione migliorata fornita per il problema chiuso #34385 nella release 1.4.42. È stato aggiunto il codice di controllo e gestione delle eccezioni isCanceled per rendere più robusta la coda delle operazioni.

**Versione 1.4.43**

* (ZD#32990) - iOS: Riproduzione dei contenuti invece degli annunci su alcuni cue point. `selectedMediaOptionInMediaSelectionGroup` L&#39;API che faceva parte dell&#39;interfaccia AVPlayerItem ora è stata spostata in AVMediaSelection in iOS 11. Il problema è stato risolto utilizzando questa nuova API.

* (ZD#33683) TVSDK rimosso == suffisso dalle stringhe di metadati. Il problema è stato risolto nella logica di analisi.

* (ZD#33905) - TVSDK iOS per effettuare chiamate ai file manifest con due agenti utente. Il problema relativo all&#39;agente utente è stato risolto nella prima chiamata m3u8 (fresh install case). M3u8 ha gli stessi agenti utente per tutte le chiamate.

* (ZD#34293) - I pre-roll inseriti nei flussi LINEAR non vengono riprodotti correttamente su iOS11. Il problema è stato risolto per gli annunci preroll.

* (ZD#34684) - Quando viene applicato il criterio di salto annunci, le cornici degli annunci pre-roll vengono visualizzate per alcuni secondi. È stata introdotta una nuova API, enableVodPreroll per disabilitare la riproduzione preroll nella riproduzione del video. Il valore predefinito per questa API è &#39;Yes&#39;. L&#39;API assicura che vengano ignorate le cuciture di contenuto degli annunci nel contenuto principale.

* (ZD#34765) - Dopo aver chiamato stop(), alcuni segmenti di flussi di trasporto vengono ancora scaricati. Migliorata l&#39;API Stop() per evitare il download dei segmenti aggiuntivi.

* (ZD#34865) - Gli annunci pre-roll per livestream vengono troncati su iOS. In relazione a iOS11, e aggiungendo un controllo aggiuntivo per confermare se il flusso è pre-roll o contenuto principale, si risolve il problema.

* (ZD#35093) - È stato corretto uno scenario di failover in cui, se la variante principale del flusso non andava a buon fine all&#39;avvio (restituisce 404), la riproduzione non passava al flusso di backup.

**1.4.42 (1.4.42.118)**

* (ZD#34385) - La riproduzione si blocca con un URL errato quando si torna dall&#39;inserimento di annunci basati su segnali.

   Aumenta il numero massimo di conteggi simultanei per `CustomAVAssetLoaderOperations`, in modo che le letture del manifesto possano continuare ad essere eseguite.

* (ZD#34373) - Gli utenti finali non possono effettuare lo streaming su dispositivi collegati HDMI, quando la registrazione del flusso non è consentita.

* (ZD#32678) - TVSDK non raccoglie gli ID annunci corretti su iOS.

   L&#39;ID dell&#39;annuncio pubblicitario finale è ora acquisito nei ping VHL in caso di reindirizzamenti VAST/VMAP.

* (ZD#33904) - TVSDK non registrato per le notifiche `AVAudioSessionMediaServicesWereLostNotification` e `AVAudioSessionMediaServicesWereResetNotification`le notifiche AVFFoundation.

   `PTMediaServicesWereLostNotification` e ora `PTMediaServicesWereResetNotification` è possibile registrarsi nell&#39;App del lettore per ricevere le notifiche quando i servizi Media vengono reimpostati o persi.

* (ZD#33815) - I clienti non possono aggiornare le proprie regole CRS per la priorità e la normalizzazione senza richiedere un aggiornamento dell&#39;app.

   Sono state aggiunte le `getCRSRulesJsonURL` e `setCRSRulesJsonURL` le API a iOS TVSDK.

**Versione 1.4.41 (1.4.41.76)**

* (ZD #34464) - Problemi nella creazione dell&#39;app di riferimento con TVSDK versione 1.4.41

   A partire da questa versione, Xcode 9 è richiesto per la compilazione di TVSDK per iOS.
* (ZD #29456) - La partita di volo inizia nello stato sospeso

   È stato corretto il problema di pausa che si verificava quando il video veniva messo in pausa durante l’immissione di una riproduzione aerea.
* (ZD #30371) - L&#39;ora di inizio di AdBreak cambia quando si inseriscono più di 2 annunci nel flusso lineare

   È stato corretto l&#39;errore che si verificava durante il tentativo di riproduzione del contenuto su Apple TV, impedendo la riproduzione completa
* (ZD #32146) - Non `PTMediaPlayerStatusError` viene ricevuto alcun contenuto per HLS Live che blocca iOS 11 dev beta

   Non `PTMediaPlayerStatusError` viene ricevuto alcun contenuto HLS Live e VOD per il blocco tramite Charles (Drop connection e 403)
* (ZD #29242) - La riproduzione video Airplay non riesce con gli annunci attivati

   Quando gli annunci sono attivati e AirPlay è abilitato all’avvio della riproduzione di un video, la riproduzione video non viene mai avviata e non viene visualizzato alcun errore
* (ZD#33341) - `DRMInterface.h` attiva la generazione di avvisi in Xcode 9

   Sono stati corretti due prototipi di blocchi in `DRMInterface.h` cui mancava la parola &#39;void&#39; negli elenchi dei relativi parametri
* (ZD#31979) - Non viene compilato/eseguito quando è iOS 10 o versione successiva per iPhone 7/iPhone7+

   È stato corretto il seguente problema: la compilazione di documenti IB per versioni precedenti a iOS 7 non era più supportata
* (ZD#32920) - schermata bianca all&#39;interno di un&#39;interruzione annuncio e nessun completamento interruzione annuncio

   Quando un&#39;interruzione annuncio presenta le istanze di Annuncio e al termine di un&#39;istanza di annuncio, viene visualizzata una schermata bianca
* (ZD#32509) - Disattivazione della registrazione dello schermo iOS 11 Disattivazione della registrazione dello schermo su iOS 11

* (ZD#33179) - Errore di evento intermittente su iOS11

   È stato corretto l&#39;errore di evento su iOS 11

**Versione 1.4.40** (1.4.40.72)

* (ZD #32465) - Il lettore non è in grado di gestire le playlist unite.

   Chiama `finishLoadingWithError`(con: Errore) per la fondazione AV per provare flussi alternativi/attivare il failover.

* (ZD #31951) - Errore TVSDK durante le rotazioni della licenza.

   È stato corretto il problema di rotazione della licenza.
* (ZD #31951) - Schermata bianca all&#39;interno di un&#39;interruzione annuncio e nessun completamento interruzione annuncio.

   È stato risolto un problema per il quale gli annunci VPAID Facebook spesso restituivano più blocchi CDATA in un singolo nodo `<AdParameters>` VAST.
* (ZD #33336) - iOS TVSDK - I contenitori degli annunci non vengono compilati, nonostante la quantità di annunci restituiti da FreeWheel sia sufficiente.

   È stata creata una relazione padre-figlio tra l&#39;annuncio della sequenza e l&#39;annuncio di fallback e l&#39;ordinamento in base alla sequenza padre e all&#39;indice.

**Versione 1.4.39** (1.4.39.43)

* (ZD #32178) - La versione TVSDK per iOS non è corretta.

   L’output della versione TVSDK nei file di registro era 1.0.211. È fisso per restituire la versione corretta.

* (ZD #32199) - Caricamento annuncio pubblicitario pigro - Il video non viene visualizzato per il contenuto.

   La timeline di Adbreak locale che non veniva inizializzata in precedenza ora viene aggiornata prima dell&#39;utilizzo.

* (ZD #27528) - Video, audio o entrambi si bloccano da 1 a 45 secondi dopo l’avvio della riproduzione di una risorsa, se l’audio secondario è impostato su non predefinito su iOS 1.2.

   Preparate e informate le tracce audio in stato Pronto.

* (ZD #30411) - Se scegliete una lingua Sap secondaria, potreste ottenere risultati imprevisti come nessun audio o audio errato.

   Preparate e informate le tracce audio in stato Pronto.

* (ZD #32199) - Caricamento annuncio pubblicitario pigro - Il video non viene visualizzato per il contenuto.

   La timeline di Adbreak locale che non veniva inizializzata in precedenza ora viene aggiornata prima dell&#39;utilizzo.

* (ZD #27528) - Video, audio o entrambi si bloccano da 1 a 45 secondi dopo l’avvio della riproduzione di una risorsa, se l’audio secondario è impostato su non predefinito su iOS 1.2.

   Preparate e informate le tracce audio in stato Pronto.

* (ZD #30411) - Se scegliete una lingua Sap secondaria, potreste ottenere risultati imprevisti come nessun audio o audio errato.

   Preparate e informate le tracce audio in stato Pronto.

**Versione 1.4.38** (1.4.38.860)

* (ZD #29281) - iOS: Aggiungere AdSystem e Creative Id alle richieste CRS

Utilizzo di ID creativi e AdSystem nella richiesta CRS in base alle regole di normalizzazione CRS

* (ZD #29176) - Arresto anomalo `PTAdPolicyDeligate``satAdBreakAsWatched:position`

L&#39;arresto anomalo dovuto a AdBreak vuoto viene gestito ora.

* (ZD #30125) - Gli annunci programmatici non funzionano nella piattaforma iOS

Aggiunta del supporto per gli annunci programmatici in iOS.

* (ZD #30782) - #EXT-X-PROGRAM-DATE-TIME Notification

L&#39;evento di metadati temporizzati non viene attivato per il tag # EXT-X-PROGRAM-DATE-TIME con flussi DRM LIVE.

**Versione 1.4.37 (1.4.37.842)**

* (ZD #28950) - Problema di riproduzione VOD

Problema di riproduzione quando il tag # EXT-X-PLAYLIST-TYPE nel flusso è impostato su Evento anziché su VOD

* (ZD #29281) - iOS: Aggiungere AdSystem e Creative Id alle richieste CRS

Utilizzo di Creative Id e AdSystem nella richiesta CRS in base alle regole di normalizzazione CRS.

* [ ZD #29462) - TremorHub ad A&amp;E VOD causando un arresto anomalo nelle app iOS

**Versione 1.4.36 (1.4.36.835)**

* (ZD #29418) - I Cues con durata 0 (#EXT-X-CUE-OUT:0.000) causano l’arresto o l’arresto anomalo della riproduzione di iOS TVSDK.

Il problema è stato risolto e la riproduzione viene avviata correttamente.

* (ZD #29462) - Annuncio in VOD che causa un arresto anomalo su iOS TVSDK.

Il problema è stato risolto. IOS TVSDK sta alzando e `exception(AUDNetworkAdInfo::initWithAdId)` non la gestisce. L&#39;eccezione è dovuta a un ID annuncio vuoto.

* (ZD #29281)- Aggiungete AdSystem e Creative ID alle richieste CRS.

Includete AdSystem e CreativeId come nuovi parametri nelle richieste 1401 e 1403 (tutti gli altri parametri rimangono invariati).

**Versione 1.4.35** (1.4.35.830)

* (ZD #27830) - È necessario determinare a livello di programmazione la differenza tra sottotitoli codificati e sottotitoli in iOS.

TVSDK ora espone i due tipi che possono essere utilizzati per filtrare il tipo di didascalia richiesto.

* (ZD #29160) - I suggerimenti per gli annunci EXT-X-CUE-OUT non vengono copiati correttamente su TVSDK iOS.

Con EXT-X-CUE-OUT midroll annuncio è in riproduzione ora.

* (ZD #29100) - L&#39;app si blocca quando l&#39;utente passa alla fine di un filmato.

Risolti più arresti anomali correlati alla sincronizzazione.

* (ZD #28785), (ZD #27712) e (ZD #25076) - L&#39;app iOS si blocca durante i grandi eventi in diretta.

Risolti più arresti anomali correlati alla sincronizzazione.

**Versione 1.4.34** (1.4.34.815 per iOS 6.0+)

* (ZD #28481) - FER outage a causa della chiave errata aggiunta alla fine di un&#39;interruzione annuncio per quei flussi FER

Per un flusso FER, il tasto prima dell&#39;interruzione dell&#39;annuncio viene inserito dopo la fine dell&#39;interruzione dell&#39;annuncio. Questo problema è stato risolto aggiungendo l&#39; *ultima chiave* visualizzata alla fine dell&#39;interruzione dell&#39;annuncio.

**Versione 1.4.33** (1.4.33.803 per iOS 6.0+)

* (ZD# 21701) Attivare CRS per i sotto-conti

Abilitata inviando l&#39;URL creativo originale per la richiesta CRS 1401 invece dell&#39;URL normalizzato, come da requisito per il back end CRS.

* (ZD# 26218) - Problema di caricamento PSDKResources.bundle

Questo problema è stato risolto aggiornando il caricamento delle risorse per cercare da tutti i bundle disponibili.

* (ZD# 27460) Prima chiamata ad annuncio Midroll - POST alla `cdn.auditude.com` restituzione 403.

Il nuovo account CDN non è in grado di gestire una richiesta POST CDN. Questo problema è stato risolto aggiornando il codice per fare in modo che la richiesta di `cdn.auditude.com` annuncio fosse GET invece di POST.

**Versione 1.4.32** (1.4.32.792 per iOS 6.0+)

* (ZD# 27132) Supporto per i valori decimali per VMAP Ad Breaks.

Quando il contenuto non era segmentato lungo le interruzioni pubblicitarie definite, i numeri interi causavano inserimenti pubblicitari imprevisti. Il problema è stato risolto non convertendo i valori decimali in numeri interi.

* (ZD# 27189) Il contenuto AES con il tag EXT-X-DISCONTINUITY-SEQUENCE non viene riprodotto correttamente.

Il problema è stato risolto inserendo il tag all&#39;inizio della playlist.

**Versione 1.4.31** (1.4.31.785 per iOS 6.0+)

* (ZD# 24528) Implementare le metriche di utilizzo TVSDK per la fatturazione

Per ulteriori informazioni, vedi Metriche []di fatturazione.

* (ZD# 24642) Supporto Picture-in-Picture per TVSDK

La funzione picture-in-picture, che in alcuni casi non funzionava correttamente, è stata corretta.

* (ZD# 25246) Segnali di interruzione annuncio non corretti

Questo problema è stato risolto allineando i tag di discontinuità tra i vari manifesti.

* (ZD# 26218) Il processo di creazione dell&#39;applicazione si complica quando si tenta di includere PSDKLibrary.framework nel framework dell&#39;applicazione del cliente

Questo problema è stato risolto creando il pacchetto PSDKLibrary.framework come richiesto.

* (ZD# 26364) Supporto multi-CDN per annunci CRS

Per ulteriori informazioni, consultate Supporto per più CDN per CRS Ad Delivery.

* (ZD# 27028) Ritardo nella riproduzione di alcuni flussi in iOS 10.

Questo problema è stato risolto fornendo una soluzione alternativa per i flussi che non hanno un&#39;estensione M3U8.

**Versione 1.4.30** (1.4.30.754 per iOS 6.0+)

In questa versione sono stati risolti i seguenti problemi per TVSDK:

* (ZD# 24180) Aggiungere un&#39;intestazione personalizzata alla whitelist

Una nuova intestazione personalizzata è stata aggiunta alla whitelist TVSDK.

* (ZD# 25016) Il flusso di failover viene selezionato in modo casuale quando vengono impostati i parametri di controllo ABR

Questo problema è stato risolto mantenendo i flussi ABR in ordine quando le impostazioni ABR vengono fornite con l&#39;impostazione initialBitrate su un flusso che include gli URL di failover. In questo modo si evitano di riprodurre i flussi di failover invece del flusso principale.

* (ZD# 25076) Arresto anomalo su PTAuditudeAdResolver loadComplete

È stato corretto il problema in cui si verificava un arresto anomalo durante l&#39;avvio/arresto rapido di più istanze PTMediaPlayer con gli annunci.

* (ZD# 25960) Nessun altro tag con sottoscrizione che attiva la trasmissione delle notifiche di modifica dei metadati

Problema per cui un tag con sottoscrizione non viene notificato quando viene visualizzato prima che sia stato risolto il primo segmento nel manifesto.

* (ZD# 26084) PSDK che genera un 106000.101000.Decoder -11833 non trovato errore durante la transizione dall&#39;ultimo annuncio al contenuto dell&#39;intrattenimento

Quando l&#39;ora di inizio dell&#39;ultima interruzione annuncio dal VMAP cade prima del completamento della durata totale, in alcune condizioni, la chiave non viene inserita fino alla fine dell&#39;ultima interruzione annuncio. Questo problema è stato risolto.

* La libreria Video Heartbeat (VHL) è stata aggiornata alla versione 1.5.9 per risolvere i seguenti problemi:

* (ZD #22351) VHL - Analytics: Durata risorsa video dal vivo

Questo problema è stato risolto aggiungendo l’API assetDuration a PTVideoAnalyticsTrackingMetadata per aggiornare la durata delle risorse per i flussi Live/Linear e fornire una logica per il controllo del flusso live.

* (ZD# 22675) VHL - Analytics: Aggiornamento della durata della risorsa video in diretta

Questo problema è lo stesso di ZD #22351.

* (ZD #25908) VHL - Analytics: Arresto anomalo evento Adobe Heartbeat

Questo problema è stato risolto aggiornando l&#39;implementazione per utilizzare la versione più recente di VHL per iOS versione 1.5.9 per migliorare stabilità e prestazioni.

* (ZD #25956) VHL - Analytics: Arresto anomalo durante la riproduzione ripetuta dei video

Questo problema è lo stesso di ZD #25908.

**Versione 1.4.29** (1.4.29.743)

* (ZD# 23901) Gli annunci di terze parti non vengono riprodotti

Questo problema è stato risolto passando alla struttura URL CRS v3 per includere l&#39;ID di zona nell&#39;URL di reinserimento.

* (ZD #25183) Problemi con la riproduzione DRM su tvOS e iOS

Questo problema è stato risolto fornendo il supporto per più tag chiave necessari per il supporto per più DRM.

* (ZD# 25334) TVSDK non riproduce un contenuto condiviso cDVR

Questo problema è stato risolto impedendo a TVSDK di convertire stringhe vuote in URL assoluti.

* (ZD# 25347) Impostate l’intestazione HTTP personalizzata su AVURLAsset

È stato aggiunto il supporto per intestazioni personalizzate sulle richieste di segmento tramite la classe PTNetworkConfiguration.

**Versione 1.4.28** (1.4.28.722)

* (ZD #24549) Chiamate multiple per il tracciamento degli annunci

Questo problema è stato risolto aggiornando il gestore della cronologia per ascoltare le notifiche su un oggetto specifico quando vengono creati più lettori.

* (ZD #24758) PTManifestLogger non supporta iOS 8

Questo problema è stato risolto aggiornando la libreria dell&#39;utilità logger alla destinazione di distribuzione della versione 7.0.

* (ZD #24775) Flusso ritardato dovuto agli annunci

Questo problema è stato risolto calcolando correttamente la deriva della durata nelle playlist dell&#39;evento.

* (ZD #24799) Alcuni episodi non vengono riprodotti nell&#39;app iOS

Questo problema è stato risolto utilizzando il server Web locale per i sottotitoli quando i file WebVTT sono soggetti a restrizioni geografiche.

**Versione 1.4.27** (1.4.27.711) per iOS 6.0+

* (ZD #24089) - Ottimizzazioni per la risoluzione di annunci su flussi DVR lunghi

Questo problema è stato risolto aggiungendo più ottimizzazioni per ridurre il tempo necessario per elaborare la finestra DVR in flussi live/lineari.

* (ZD #21554) - Segnali di errore TVSDK non attivati per il tipo di applicazione = video/mp4

Questo problema è stato risolto abilitando il lettore a ping degli URL di tracciamento errori corretti in formati di risorse non validi.

* (ZD #24424) - L&#39;arresto anomalo di tipo EXC_BAD_ACCESS KERN_INVALID_ADDRESS proviene dall&#39;interno di PSDKLib per iOS su dispositivi hardware più recenti.

È stato corretto l’arresto anomalo che si verificava a causa di un’istanza del lettore multimediale non allocata, quando la riproduzione veniva scambiata rapidamente tra flussi diversi.

* (ZD #24575) - Arresto anomalo in TVSDK sui dispositivi a 32 bit quando enableDebugLog=true

È stato corretto il problema nel formato di registro che causava l’arresto anomalo sui dispositivi a 32 bit quando la registrazione è abilitata.

**Versione 1.4.26** (1.4.26.702) per iOS 6.0+

* (ZD# 20213) - TVSDK FW deve essere dinamico/modularizzato per XCode7

Risolto aggiornando le librerie con il supporto del modulo

**Versione 1.4.25** (1.4.25.684) per iOS 6.0+

* (ZD #19629) - Pausa video dal vivo durante l&#39;ingresso di Airplay ad ATV 4

Questo problema è stato risolto aggiungendo un periodo di attesa dopo aver rimosso gli elementi obsoleti ma prima di aggiungere nuovi elementi a AVQueuePlayer. Senza il periodo di attesa, le notifiche vengono inviate all&#39;elemento errato.

* (ZD #19856) - Non vengono visualizzati sottotitoli se attivati per impostazione predefinita

Sono stati corretti i problemi relativi alla playlist Web, che causavano la visualizzazione errata dei sottotitoli.

* (ZD #21590) - Prestazioni video e tracciamento nelle ultime build di origine

È stato corretto il problema della lunghezza video mancante in VideoAnalytics.

* (ZD #20202) - L’impostazione dello stile dei sottotitoli personalizzati provoca l’arresto anomalo dell’app iOS

Questo problema è stato risolto aggiungendo ulteriori controlli oggetti null durante l&#39;impostazione degli stili dei sottotitoli.

* (ZD #20709) - Lunghezza video indicata come 0 nel tracciamento dell’avvio del video

Questo problema è lo stesso di (ZD #21590).

* (ZD #22280) - La lunghezza video di Analytics è impostata su 0

Questo problema è lo stesso di (ZD #21590).

* (ZD #22592) - Problemi con la riproduzione aerea in Primetime

Questo problema è lo stesso di (ZD #19629).

* (ZD#22922) - Commutazione del bitrate manuale per iOS

Questo problema è stato risolto fornendo un&#39;opzione per specificare il bitrate massimo.

* (ZD #23084) - Conformità Apple per le reti solo IPv6

I simboli non consigliati da Apple per la compatibilità IPv6 sono stati rimossi.

**Versione 1.4.24** (1.4.24.661) per iOS 6.0+

* ZD #2548) - Supporto Primetime per la pubblicità interattiva su dispositivi mobili - VPAID 2.0

Questo problema è stato risolto aggiornando la logica per scoprire la visualizzazione del lettore se un annuncio VPAID non viene riprodotto correttamente.

* (ZD #20101) - L&#39;implementazione personalizzata del capitolo attiva l&#39;evento di inizio del capitolo durante la riproduzione dell&#39;annuncio

Questo problema è stato risolto aggiornando VideoAnalyticsTracker per rilevare correttamente l’inizio/il completamento del capitolo durante la transizione tra i limiti dei capitoli e non dei capitoli.

* (ZD #20784) - Analytics: Attivazione di contenuti completi per transizioni video live

Questo problema è stato risolto aggiungendo una logica per attivare manualmente il completamento del contenuto durante una sessione di tracciamento video.

Sono state aggiornate le seguenti librerie:

* Libreria AdobeMobile alla versione 4.10.0
* Libreria VHL a 1.5.6
* Libreria VHL-Nielsen a 1.6.7
* (ZD #21855) - I sottotitoli non vengono riprodotti dopo il mid-roll

In questo problema, i tag di discontinuità duplicati causavano la mancata visualizzazione dei sottotitoli dopo il mid-roll. Questo problema è stato risolto rimuovendo i tag di discontinuità che si trovano l&#39;uno accanto all&#39;altro.

* (ZD #21994) - Stringa fuori limite nelle sezioni PTHLSU

La causa più probabile dell&#39;arresto anomalo è rappresentata da un URL racchiuso tra virgolette in una chiave EXT-X.

* ZD #22074) - L&#39;arresto anomalo dell&#39;AUDVAST si verifica una volta al minuto su iOS

Nella versione 1.4.23, l&#39;arresto anomalo causato dalla presenza di caratteri non sicuri in un URL di reindirizzamento VAST è stato risolto. Tuttavia, TVSDK continuava a saltare questi annunci.

Questo problema è stato risolto gestendo i caratteri non sicuri e consentendo la riproduzione degli annunci.

* (ZD #22694) - PTMediaPlayer.  Vista nascosta dal lettore

Questo problema è stato risolto aggiornando la logica per scoprire la visualizzazione del lettore se un annuncio VPAID non viene riprodotto correttamente.

**Versione 1.4.23** (1.4.23.641) per iOS 6.0+

* (ZD #18016) - Nessuna risposta da Primetime SDK con una condizione di rete non valida

Questo problema è stato risolto migliorando la notifica di errore quando si verifica un errore irreversibile da AVFFoundation e per consentire all&#39;app di gestire il riavvio dopo l&#39;errore.

* (ZD #20580) - Arresto anomalo in PTSplicerManager

Questo problema è stato risolto fornendo ulteriore protezione dai problemi di concorrenza che causano l&#39;arresto anomalo.

* (ZD #21782) - Codice di errore iOS 10100

È stato corretto il problema per cui TVSDK restituiva un errore 101000 durante l&#39;avvio della riproduzione sui flussi DRM di Adobe Access.

* (ZD #21889) - La riproduzione di annunci online e contenuti offline non riesce

È stato corretto il seguente problema: la riproduzione non riusciva dopo che un annuncio pubblicitario su contenuto offline crittografato con AES.

* (ZD #22074) - L&#39;arresto anomalo dell&#39;AUDVAST si verifica una volta al minuto su iOS

Questo problema è stato risolto migliorando la gestione dei tag di annunci VAST di terze parti con caratteri non validi nell&#39;URL.

* (ZD #22257) - Il TVSDK non riproduce il flusso DRM

È stato corretto il problema per cui il TVSDK che restituiva un errore 101000 durante l&#39;avvio della riproduzione sui flussi DRM di Adobe Access.

**Versione 1.4.22** (1.4.22.627) per iOS 6.0+

* (ZD #18709) - Arresto anomalo di TVSDK per iOS

È stato corretto il problema di arresto anomalo che si verificava in alcuni flussi protetti da DRM di Adobe Access.

* (ZD #18850) - Aggiornare la logica di selezione creativa in base alle regole CRS

Questo problema è stato risolto aggiungendo un file di configurazione .json per specificare la priorità di selezione creativa.

* (ZD #19770) - Il feed video AES protetto non viene più riprodotto

È stato corretto il problema per cui alcuni 302 flussi reindirizzati non venivano riprodotti.

* (ZD #19629) - Pausa video dal vivo durante l&#39;ingresso di Airplay ad ATV 4

Questo problema è stato risolto aggiungendo una soluzione alternativa per la messa in pausa dei video in diretta quando la riproduzione audio è attivata per i dispositivi Apple TV 4. Il problema sembra essere relativo ad AppleTV 4.

* (ZD #21119) - Il TVSDK viene bloccato dopo la riproduzione di un annuncio

È stato aggiunto il supporto per i flussi crittografati AES con una sequenza IV durante l&#39;utilizzo dell&#39;inserimento di annunci.

* (ZD #21125) - Ritorno dall&#39;annuncio live/lineare all&#39;inizio

È stato aggiunto il supporto per il ritorno da un&#39;interruzione pubblicitaria prima che l&#39;interruzione dell&#39;annuncio venga riprodotta fino al completamento. La restituzione anticipata è indicata tramite un tag manifest personalizzato.

* (ZD #21224) - Supporto Airplay per flussi token da Akamai

Sono state aggiunte delle API alla classe PTNetworkConfiguration per aggiungere i cookie come parametri URL ai segmenti per determinati flussi di token Akamai.

* (ZD #21287) - Registro estraneo

È stato risolto un problema relativo ad alcune istruzioni di registro visualizzate per impostazione predefinita nella console xcode anche quando la registrazione è disabilitata.

* (ZD #21446) - Gli eventi Ad Break a volte non attivati da TVSDK

Sui flussi EVENT, le interruzioni pubblicitarie non vengono attivate correttamente nella build precedente. Questa build risolve il problema.

**Versione 1.4.21** (1.4.21.605) per iOS 6.0+

* (ZD #20749) - Fallback salta le risposte VAST non vuote; Altri URL di tracciamento annunci attivati

È stato risolto un problema relativo ai ping duplicati negli annunci di fallback.

**Versione 1.4.20** (1.4.20.590) per iOS 6.0+

* (ZD #18639) - Il TVSDK utilizza CPU/risorse eccessive su una lunga risorsa per la registrazione a caldo

L&#39;utilizzo eccessivo di CPU/risorse è stato corretto nei due livelli. In primo luogo, consentendo l&#39;esecuzione della funzione di aggiornamento del tempo su una coda globale, invece del thread principale, e ottimizzando l&#39;utilizzo della CPU per l&#39;analisi del manifesto con il m3u8 precedentemente elaborato e memorizzato nella cache.

* (ZD #19349) - Gli annunci pre-roll vengono ignorati durante la limitazione della connessione di rete.

Questo problema è stato risolto fornendo un evento di timeout (requestTimeout) all’applicazione e agli adMetadata.  l&#39;API adRequestTimeout per ignorare il timeout predefinito di 10 secondi.

* (ZD #19446) - Notifica mancante nei flussi in diretta

Questo problema è stato risolto consentendo la sottoscrizione dell’applicazione al programma EXT-X-PROGRAM-DATE-TIME sui flussi live.

* (ZD #19459) - Arresto anomalo durante la preparazione di audio alternativo con PTMediaPlayerItem PrepareAudioOptionsWithAVMediaSelectionOptions
* (ZD #19460) - Arresto anomalo - `[PTMediaPlayerItem prepareSubtitlesOptionsWithAVMediaSelectionOptions:nonForcedOptions:]`

Questo problema è lo stesso di Zendesk #19459.

* (ZD #19574) - TVSDK non restituisce i dati di risposta M3U8 per il contenuto DRM o non DRM

Nel caricamento iniziale del file manifesto in PTMediaPlayerItem.PreparaToPlay, se il caricamento del manifesto non è riuscito, TVSDK non segnala il corpo della risposta di errore all’applicazione.

Questo problema è stato risolto consentendo al TVSDK di segnalare la risposta di errore come un errore all&#39;applicazione.

* (ZD #19615) - La logica di fallback non funziona

Nell&#39;implementazione corrente, gli annunci di fallback venivano ignorati e non venivano ricompilati a meno che questi annunci non fossero in formato m3u8. Questo problema è stato risolto aggiungendo anche il supporto per la ricompilazione di annunci di fallback.

* (ZD #19770) - TVSDK non riproduce alcun contenuto AES protetto con reindirizzamento 302

Il problema di reindirizzamento è stato risolto perché l&#39;URL di reindirizzamento veniva eliminato da CleanConnectionData prima che potesse essere utilizzato per analizzare il manifesto.

* (ZD #19856) - I sottotitoli non vengono visualizzati per alcuni bitrate se attivati per impostazione predefinita

Questo problema è stato risolto gestendo l&#39;errore da iOS per i segmenti dei flussi in cui i sottotitoli non vengono visualizzati.

* (ZD #19868) - Il TVSDK si arresta in modo anomalo quando viene trafficato un creativo non valido

È stato corretto l&#39;arresto anomalo nel TVSDK per la deallocazione errata di un&#39;istanza del parser esteso.

* (ZD #20180) - Gli annunci VPAID vengono saltati occasionalmente

Il tipo mime JavaScript non veniva sempre incluso o considerato come un tipo mime valido. Questo problema è stato risolto includendo JavaScript come tipo mime valido.

* (ZD #20749) - Fallback salta le risposte VAST non vuote; Altri URL di tracciamento annunci attivati

È stato risolto il problema per il quale alcuni dei creativi non venivano reinseriti in pacchetti.

**Versione 1.4.19** (1.4.19.563) per iOS 6.0+

* ZD #18639) - Il TVSDK utilizza CPU/risorse eccessive su una lunga risorsa per la registrazione a caldo

Questo problema è stato risolto ottimizzando la riscrittura della playlist DRM m3u8 ai bit cache della playlist precedentemente riscritti. Questo è più importante quando si riproducono flussi m3u8 live per i quali m3u8 viene scaricato dopo ogni download di segmento.

* (ZD#18956) - player.drmManager è nil quando il punto di interruzione è impostato in iOS Demo Player

Questo problema è stato risolto aggiornando l&#39;implementazione API PTMediaPlayer.drmManager per recuperare DRMManager dal framework DRM.

**Versione 1.4.18** ( 1.4.18.557) per iOS 6.0+

* (ZD #18844) Tracciamento dell&#39;indicatore di riproduzione per il contenuto live nel lettore iOS.

Questo problema è stato risolto consentendo alle applicazioni di impostare il proprio valore della testina di riproduzione.

* (Zendesk #18518) - Se il nome del video non è specificato, per impostazione predefinita il nome di TVSDK è * lettore basato su PSDK.*

Questo problema è stato risolto rimuovendo il valore predefinito per il nome del lettore.

**Versione 1.4.17** (1.4.17.545) per iOS 6.0+

* (Zendesk #2228) - Migliorate TVSDK per restituire la risposta JSON del recupero di un manifesto

Invece di inviare un errore quando il contenuto non è M3U8, DRM Framework restituisce un DRMMetadata nil. Il problema è stato risolto aggiungendo metadati per esporre il contenuto quando si verifica la notifica M3U8_PARSER_ERROR.

* (Zendesk #2231) - Errore restituito dal recupero del manifesto non disponibile in MediaPlayerNotification

Stessa risoluzione di Zendesk #2228

* (Zendesk #3304) - VAST 3.0 `[ERRORCODE]` macro non popolata

Problema per il quale l’SDK di Auditude non riesce a inviare un ping quando l’URL di tracciamento ha degli spazi all’inizio è stato risolto.

* (Zendesk #17294) - Arresto anomalo di SecKeyRawSign

È possibile che si verifichi un arresto anomalo quando il codice del cliente utilizza la catena di chiavi.

* (Zendesk #18008) - Cookie di supporto per iOS8+ per il supporto di flussi token

I flussi token Akamai richiedono che i cookie vengano inviati sulle richieste dei segmenti, e questo non era possibile su iOS 7 e versioni precedenti. A partire da iOS 8, Apple ha aggiunto un&#39;API che consente il passaggio di cookie per le richieste di segmenti. Questo supporto è ora disponibile in TVSDK. È stato inoltre aggiunto il supporto per l’invio di un agente utente, se disponibile.

* (Zendesk #18166) - TVSDK 1.4.15 invia centinaia di avvisi durante la compilazione con DWARF con opzioni di file dSYM

Tutti gli avvisi sono stati risolti.

**Nota**: per TVSDK sono state aggiunte librerie compatibili con tvOS.

**Versione 1.4.16** (1.4.16.1454)

* Zendesk #3875 - Tabulazione S Arresti anomali durante la riproduzione

Ripristino della dipendenza di OKHTTP dall’auditude per CRS in quanto TVSDK ora utilizza direttamente la connessione httpurlconnection invece di curl. Il problema è stato risolto eliminando le eccezioni prima di effettuare un&#39;altra chiamata JNI.

* (Zendesk #4487) - Tracciamento del canale lineare dei contenuti

Il problema è stato risolto inizializzando nuovamente il tracciatore heartbeat video durante una sessione di riproduzione del flusso lineare.

* (Zendesk #17919) - Android - la ricerca del contenuto causa un errore heartbeat

Il problema era quello di risolvere il heartbeat in stato di errore in caso di ricerca in un capitolo

* (Zendesk #18053) - L’applicazione che utilizza l’SDK TVSDK si blocca su Marshmallow

Il TVSDK si arrestava in modo anomalo su Android M OS quando la libreria TVSDK utilizza il codice neon che esegue la conversione colore YUV `->` RGB. Questo problema è stato risolto aggiornando le funzioni che causano il problema utilizzando la versione non neon di `code`.

* (Zendesk #18072) - Android M - Arresto anomalo dell&#39;applicazione

Questo arresto anomalo si verifica quando si chiamano le API MediaCodecList e MediaCodecInfo quando si verifica se il profilo e il livello sono supportati. Adobe sta cercando il supporto di Google per ulteriori informazioni. Questo problema è stato risolto fornendo una soluzione temporanea caricando tutte le informazioni del codec in anticipo per evitare di chiamare queste API solo quando sono necessarie informazioni sul codec.

* (Zendesk #18074) - Sottotitoli arabi non funzionanti su Nexus con Android 6.0

Questo problema è stato risolto fornendo il supporto per la mappa dei font CTS per Android.

**Versione 1.4.15** (1.4.15.512) per iOS 6.0+

**Nota**: Il modulo Nielsen è stato rimosso dalla build TVSDK, ma il TVSDK verrà aggiornato prossimamente con un nuovo modulo di integrazione Nielsen.

* (ZD #2228) - Errore restituito dal recupero del manifesto non disponibile in MediaPlayerNotification

Sono stati aggiunti metadati per esporre il contenuto quando si verifica la notifica M3U8_PARSER_ERROR.

* (ZD #4437) - Arresti anomali in Adobe Primetime SDK

È stato corretto un arresto anomalo segnalato durante la preparazione di sottotitoli o audio alternativo.

* (ZD #4487) - Tracciamento del canale lineare dei contenuti

È possibile riinizializzare il tracciatore heartbeat video durante una sessione di riproduzione del flusso lineare.

**Versione 1.4.14** (1.4.14.498) per iOS 6.0+

* (ZD #17260) - Arresto anomalo su playlistManagerForURL

È stato corretto un arresto anomalo intermittente dovuto a problemi di concorrenza.

**Versione 1.4.13** (iOS 6.0+)

* (ZD #3304) - VAST 3.0 `[ERRORCODE]` macro non popolata

   * Il codice di errore 400 sarà esposto se l&#39;annuncio in linea ha un cattivo creativo.
   * `[ERRORCODE]` la macro verrà codificata nell&#39;URL.

* (ZD #3865) Integrazione Heartbeat con gli annunci IMA

È stato corretto un bug a causa del quale la lunghezza del video veniva riportata in modo non corretto.

* È stato aggiornato il lettore demo TVSDK per supportare iOS 9

Per supportare correttamente iOS 9, è necessario configurare le eccezioni di Application Transportation Security. Ai fini della demo, l&#39;ATS è completamente disattivato.

**Versione 1.4.12** (1.4.12.464) per iOS 6.0+

* (ZD #4521) Test CRS lato client e SSAI

È stato corretto MD5 inverso errato nell’URL 3P.

**Versione 1.4.12** (1.4.12.463) per iOS 6.0+

* (ZD #2751) CSAI e CRS / Miglioramento: Gestire gli elementi dinamici in alcuni URL di file multimediali.

Creative Repackaging Service è stato aggiornato per gestire correttamente gli annunci con URL creativi dinamici.

* (ZD #3654) Perdita di memoria nella versione PSDK dopo 1.3.4.166

È stata corretta una perdita di memoria in drmFramework con riproduzione regolare su dispositivi iOS 8.2

* (ZD #3988) Preroll viene ignorato quando si tenta di rientrare in esso dopo la prima riproduzione

È stato corretto un bug a causa del quale i criteri degli annunci potevano essere disattivati correttamente.

* (ZD #4017) Richiesta di API iOS per forzare la riproduzione di annunci nella ricerca precedente

Risolto con correzione per ZD #4279

* (ZD #4279) HLS TVSDK inserimento di annunci -302 problema di reindirizzamento su iOS e desktop

È stato corretto un bug a causa del quale una risorsa annuncio utilizzava un URL di reindirizzamento relativo

**Versione 1.4.9** (1.4.9.427) per iOS 6.0+

* (ZD #3075) Problema di raggiungibilità di Internet - iOS

È stata aggiunta una notifica per rilevare quando la riproduzione è bloccata.

* (ZD #3193) Richiesta di una modifica di profilo API in TVSDK

Aggiornato PTPlaybackInformation per esporre il valore indicatoBitrate aggiornato. Aggiornata la notifica BITRATE_CHANGE per garantire un tempo più affidabile e preciso rispetto ai bitrate segnalati da M3U8.

* (ZD #3324) Problemi di segnalazione di annunci Primetime in assenza di supporti pubblicitari in VMAP

Supporto per il ping di URL vuoti per il tracciamento delle interruzioni di annunci, TVSDK verificherà ora l&#39;avvio dell&#39;interruzione di annunci e completerà i ping per le interruzioni di annunci vuote.

**Versione 1.4.8** (1.4.8.402)

* (ZD #3158) Arresto anomalo di IOS 7 in Riproduzioni evento complete

**Versione 1.4.7** (1.4.7.382)

* (ZD #2197) Tracciamento degli errori degli annunci. Aggiunta notifica per la risorsa non riuscita a caricare il manifesto.
* (ZD #2894) Player Esegue 4 richieste di manifesto di livello principale durante la riproduzione.
* (ZD #2992) Auditude Segnalare durate e identificatori bizzarri.

**Versione 1.4.6**(1.4.6.325)

* (ZD #2197) Tracciamento degli errori degli annunci. Aggiunta notifica per il caricamento del manifesto della risorsa non riuscita

**Versione 1.4.5** (1.4.5.283)

* (ZD #2141) Implementazione di Analytics per l&#39;app TreeHouse, aggiunta della `AdobeAnalyticsPlugin.a` libreria per creare il pacchetto.
* Video Heartbeats Library update to 1.4.1.2
* [PTPALY-4226] [relativo a ZD #2423] L&#39;esecuzione della reimpostazione DRM può comportare l&#39;eliminazione dei dati del documento dell&#39;applicazione.

**Versione 1.4.4** (1.4.4.242)

* Video Heartbeats Library (VHL) aggiornato alla versione 1.4.1.

* (ZD #2435) Documentazione TV SDK sui requisiti di analisi

**Versione 1.4.2** (1.4.2.210: iOS 6.0+)

* (ZD #1129) `_player.currentItem.audioOptions` Ritorno vuoto
* (ZD #2109) Primetime PSDK 1.4.1.125 non funziona con Xcode 5.1.1
* (ZD #2137) Arresto anomalo in PSDK su iOS quando non è possibile caricare i metadati DRM

**Versione 1.4.1**(1.4.1.125)

* (ZD #1107) Simboli duplicati del lumberjack
* (ZD #1644) Modificare l&#39;agente utente iOS per il targeting e il reporting
* (ZD #1850) File Lumberjack del cacao inclusi nell’SDK iOS
* (ZD#1908) I tag personalizzati vengono ignorati da PSDK se sono presenti più di 1

**Versione 1.4.0** (1.4.0.32)

* Zendesk #1024 - Funzione per rimuovere gli annunci dal flusso tramite manifesto

## Certificazione e supporto dei dispositivi {#device-certification-and-support}

>[!NOTE]
>
>Le seguenti funzionalità **non** sono supportate in TVSDK:
>
>* Slow motion, su qualsiasi piattaforma o versione.
>* Giochi di trucchi dal vivo.


**Versione 1.4.43**

* TVSDK 1.4.43 è certificato per iOS 11.

**Versione 1.4.29**

* TVSDK 1.4.29 è stato certificato per iOS 10.

**Versione 1.4.28**

* TVSDK 1.4.28 è stato certificato per iOS 10 Beta 7.
* Supporto DRM per imporre il protocollo HTTPS mediante l&#39;aggiunta `forceHTTPS` di `isForcingHTTPS` API e API.
* Sono state aggiornate le librerie VHL a 1.5.8, le librerie Adobe Mobile a 4.8.4 e la libreria dell&#39;utilità logger alla versione 7.0 della destinazione di distribuzione.

**Versione 1.4.19**

Questa versione di TVSDK è stata certificata con il supporto FairPlay per iOS e tvOS.

**Versione 1.4.17**

* tvOS

   Questa versione di TVSDK include il supporto per tvOS ed è stata certificata per flussi HLS non crittografati.

   **Nota**: Ricorda le seguenti linee guida per la compilazione:

   * Il supporto TVSDK tvOs è limitato ai flussi crittografati non Adobe DRM. È necessario rimuovere il riferimento a drmNativeInterface.framework nelle impostazioni di build tvOS. I flussi crittografati AES sono ancora supportati.
   * Apple richiede che tutte le applicazioni Apple TV siano abilitate per il bitcode, pertanto è necessario attivare questo flag nelle impostazioni del progetto.

## Problemi noti e limitazioni {#known-issues-and-limitations}

* A causa della deprecazione della classe iOS UIWebView, in iOS TVSDK 3.6 a partire:
   * Gli annunci VPAID non verranno riprodotti come previsto in iPad 13.
   * Gli annunci pubblicitari non verranno riprodotti come previsto.

* In iOS TVSDK, tutti gli annunci vengono inseriti nel manifesto del contenuto. I comportamenti degli annunci vengono implementati ricercando in base alla durata del contenuto e dei segmenti degli annunci. Quindi, se le durate del segmento non sono precise, la ricerca potrebbe non terminare sempre al fotogramma esatto dell&#39;inizio o della fine dell&#39;interruzione dell&#39;annuncio. Anche se le durate sono al frame, c&#39;è una tolleranza che la piattaforma stessa impone alla ricerca e ci possono essere alcuni fotogrammi o annunci o contenuto visualizzati. Si tratta di una limitazione della piattaforma e del modo in cui l’inserimento di annunci funziona con TVSDK su iOS.
* La decisione di saltare avviene sull&#39;evento di ricerca in questo caso. Tuttavia, poiché le durate del segmento di annuncio nel manifesto non rappresentano con precisione la durata effettiva dell&#39;annuncio, la ricerca non è accurata per i fotogrammi. Di conseguenza, quando vengono applicati i criteri degli annunci vengono visualizzati alcuni frame degli annunci.
* È possibile che il video a rotazione licenza non venga riprodotto su iOS 11 e che venga riprodotto correttamente su iOS 9.x e iOS 10.x.
* Nel supporto VPAID 2.0, se la riproduzione è attiva su AirPlay, gli annunci VPAID vengono ignorati.
* drmNativeInterface.framework non si collega correttamente quando la destinazione minima è impostata su iOS7 (o versione successiva).
Soluzione: Specificate esplicitamente la libreria libstdc+.6.dylib come segue: Vai a Target->Fasi build->Collega binario a librerie e aggiungi libstdc++.6.dylib.
* Post-Roll Ad non viene inserito per l&#39;API di sostituzione.
* La ricerca di un’interruzione di annuncio (senza uscire da essa) genera una notifica duplicata di inizio e interruzione di annuncio
* L&#39;impostazione currentTimeUpdateInterval non ha alcun effetto.
Nota: In alcune versioni iOS, il sistema operativo non carica automaticamente le risorse all&#39;interno di PSDKLibrary.framework. È importante copiare manualmente il file PSDKResources.bundle nelle risorse del bundle dell’applicazione: Andate a &quot;Fasi build&quot; e copiate le risorse del bundle.
* L&#39;app di riferimento non può essere creata utilizzando Xcode 8 o versioni precedenti. A partire da iOS TVSDK versione 1.4.41, utilizzate Xcode 9 per la compilazione.
* Gli annunci VPAID non rispettano il valore delayAdLoadingTolerance.
* 24077 - Per alcuni contenuti HLS con sottotitoli, il lettore si arresta in modo anomalo quando si esegue il metodo Stop o Reset.
* Le notifiche di errore dettagliate non sono disponibili nel caso in cui la risoluzione Just in Time Ad sia abilitata.
* Le notifiche di errore vengono registrate in base al tempo di risoluzione degli annunci e non in base alla sequenza degli annunci.
* Il supporto HEVC presenta le seguenti limitazioni in questa versione
   * DRM non supportato
   * Supporto CC (CEA 608/708) non disponibile perché non supportato in CMAF.
   * Il supporto 4K non è ancora presente.
   * I tag ID3 non sono supportati perché non sono supportati in CMAF.
   * Flussi HEVC live non muxed non verificati.
   * Supporto HEVC Ads non verificato.
* Con JIT abilitato e tolleranza impostata su 10 secondi, non viene visualizzata alcuna chiamata VAST per la prima interruzione di annuncio nel caso di VMAP->VAST annunci di reindirizzamento.
* Per il corretto funzionamento della risoluzione degli annunci, ogni volta che la playlist viene aggiornata durante la riproduzione dello streaming live, il lettore si aspetta una playlist cucita entro 20 secondi. Se non riceve una playlist cucita entro tale intervallo, viene generato un errore interno e il lettore si arresta.

## Risorse utili {#helpful-resources}

* [TVSDK 3.4 per iOS Programmer&#39;s Guide](https://docs.adobe.com/content/help/en/primetime/programming/tvsdk-3x-for-ios/introduction/ios-3x-overview.html)
* [Riferimento API per TVSDK iOS 3.4](https://help.adobe.com/en_US/primetime/api/psdk/appledoc_v34/index.html)
* Consulta la documentazione completa della guida nella pagina Informazioni e supporto [di](https://helpx.adobe.com/support/primetime.html) Adobe Primetime.
