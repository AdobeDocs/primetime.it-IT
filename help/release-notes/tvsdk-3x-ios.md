---
title: Note sulla versione di TVSDK 3.13 per iOS
description: Le note sulla versione di TVSDK 3.13 per iOS descrivono le novità o le modifiche, i problemi risolti e noti e i problemi del dispositivo in TVSDK iOS 3.13.
exl-id: adf8ab23-86d6-4113-b243-2709d5f7f829
source-git-commit: 59ea8008c828f3bdf275fea5cc2a59c37b0c4845
workflow-type: tm+mt
source-wordcount: '7575'
ht-degree: 0%

---

# Note sulla versione di TVSDK 3.13 per iOS {#tvsdk-for-ios-release-notes}

Le note sulla versione di TVSDK 3.12 per iOS descrivono le novità o le modifiche, i problemi risolti e noti e i problemi del dispositivo in TVSDK iOS 3.12.

## Requisiti di sistema e software {#system-software-requirements}

Prima di scaricare iOS 3.12, assicurati che le versioni di hardware, sistemi operativi e applicazioni soddisfino i seguenti requisiti:

Sistema operativo: iOS 8.0 o versione successiva.

## iOS TVSDK 3.13

Il rilascio introduce il supporto per gli annunci DEMUXED &quot;HLS/CMAF&quot; (preroll, midroll e postroll) per flussi LIVE, VOD e FER.

Per correzioni di problemi segnalati dai clienti, vedi [Problemi risolti](#resolved-issues). Per informazioni sulle limitazioni, consulta [problemi e limitazioni noti](#known-issues-and-limitations).

### Nuove funzioni e problemi risolti nelle versioni precedenti {#whats-new-previous}

**iOS TVSDK 3.12**

È stato risolto un problema a causa del quale lo streaming live non riesce dopo 15 minuti di riproduzione.

**iOS TVSDK 3.11**

Correzioni fornite per i problemi dei clienti in cui `isFallbackOnInvalidCreativeEnabled` e metodo `customParams` causare l&#39;arresto anomalo dell&#39;applicazione.

**iOS TVSDK 3.10**

* È stato risolto un problema a causa del quale il lettore TVSDK non si attivava `PTMediaPlayerStatusError` notifica quando la rete non è disponibile.

**iOS TVSDK 3.9**

* È stato risolto un problema che impediva la riproduzione dei sottotitoli VTT, causando il blocco dell’app.

* iOS TVSDK 3.9 include il certificato di trasporto di individualizzazione aggiornato.

**Hotfix di iOS TVSDK 3.8.0.83**

L&#39;hotfix aveva il certificato di trasporto di individualizzazione aggiornato.

**iOS TVSDK 3.8**

Conformità iOS 13 e gestione di iOS 13 `UIWebView` Obsolescenza dell’API.

**iOS TVSDK 3.7**

Hotfix per uno scenario in cui la riproduzione si arresta quando sono state effettuate più richieste di risoluzione di annunci simultaneamente.

**iOS TVSDK 3.6**

**Correzioni nella proprietà wideXML della classe`PTNetworkAdInfo`**

La `vastXML` la proprietà non veniva impostata correttamente e restituiva un valore nil.

**iOS TVSDK 3.5**

**Abilitazione dell&#39;audio in background**

*Configura l&#39;app per continuare a riprodurre audio quando entra in background.*

Per abilitare questa funzione, è necessario impostare la nuova API `audioPlaybackInBackground` aggiunto in `PTMediaPlayer` classe. Con questa API abilitata, l’app è pronta per riprodurre l’audio in background.

**iOS TVSDK 3.4.0.19 (Hotfix)**

Questa versione dispone di una correzione per gli arresti anomali dell&#39;applicazione che si verificano in uno scenario di failover degli annunci.

**iOS TVSDK 3.4**

**Timeout risoluzione annunci**

* Con TVSDK 3.4, gli utenti possono ora impostare il valore di timeout per la risoluzione complessiva degli annunci e i download dei manifest. Se entro un determinato timeout alcuni annunci non vengono risolti, TVSDK riproduce gli annunci rimanenti.

* `PTAdMetadata: adRequestTimeout` L’API è stata dichiarata obsoleta e verrà rimossa. Il valore predefinito è stato impostato su 35 secondi.

* Sono state introdotte due nuove API alternative nella `PTAdMetadataClass: adResolutionTimeout`  - timeout per chiamate adManifestTimeout complessive di risoluzione annunci - timeout per download di manifesti annunci.

**Ottimizzazione dei ricavi**

È stato abilitato TVSDK per identificare le aree problematiche correlate ai flussi di lavoro di inserimento annunci per creare rapporti su un punto finale di analisi.

**Versione 3.3**

TVSDK 3.3 è ora compatibile con l’SDK iOS 11. Tutte le API obsolete sono state sostituite con alternative appropriate.

**Versione 3.2**

**Supporto aggiuntivo per la registrazione (fase 2)**

È stato aggiunto il supporto per le notifiche di errore, in caso di:

* La versione HLS dell’annuncio utilizza un livello più alto del contenuto.

* È esclusa la variante solo audio.

* Richiesta VAST/VMAP non riuscita.

**Versione 3.1**

* **Supporto aggiuntivo per la registrazione**
È stato aggiunto il supporto per le notifiche descrittive in caso di errori di riproduzione di annunci.

* **Aggiunto [!DNL Fairplay] Supporto del flusso CMAF crittografato**
   [!DNL Fairplay] Sono ora supportati i flussi CMAF crittografati con riproduzione codec AVC.

**Versione 3.0.1**

Nessuna nuova funzione o miglioramento in questa versione.

**Versione 3.0**

* TVSDK 3.0 supporta flussi HEVC.

* Just In Time (Solo in tempo) - Risoluzione degli annunci più vicini ai marcatori pubblicitari.

Aggiunto `enableDelayAdLoading` proprietà di tipo booleano nell&#39;interfaccia a livello di app per abilitare JIT. Se `enableDelayAdLoading` è NO, `setadMetadata.delayAdLoading`su True (proprietà dell&#39;interfaccia PTAdMetadata).

Con questa proprietà abilitata, TVSDK risolve ogni annuncio prima della sua posizione in base al valore di tolleranza definito. Per impostazione predefinita, `delayAdTolerance` è impostato su cinque secondi.

**Versione 1.4.45**

Per rispettare Xcode10, TVSDK è stato spostato da `libstdc++` a `libc++`e di conseguenza la versione minima supportata è iOS 7. In precedenza era iOS 6.

**Versione 1.4.44**

Nessuna nuova funzione o miglioramento in questa versione.

**Versione 1.4.43**

* Esperienza simile a quella televisiva di poter partecipare al mezzo di un annuncio senza attivare il tracciamento parziale degli annunci.\
   Esempio: L&#39;utente si unisce al centro (a 40 secondi) di un&#39;interruzione pubblicitaria di 90 secondi costituita da tre annunci da 30 secondi. Questo è a 10 secondi dal secondo annuncio dell&#39;interruzione.

   * Il secondo annuncio viene riprodotto per la durata rimanente (20 sec) seguita dal terzo annuncio.
   * I tracciatori degli annunci per l’annuncio parziale riprodotto (secondo annuncio) non vengono attivati. Vengono attivati i tracker solo per il terzo annuncio.

* Aggiunto `enableVodPreroll` proprietà di tipo booleano nell&#39;interfaccia PTAdMetadata. La proprietà può essere utilizzata per abilitare il pre-roll su un flusso VoD. Se `enableVodPreroll` è NO, PSDK non riproduce pre-roll. Questo, tuttavia, non ha alcun impatto sui rulli medi. Il valore predefinito di `enableVodPreroll` È SÌ.
* `closedCaptionDisplayEnabled` API di `PTMediaPlayer` l’interfaccia è contrassegnata come obsoleta a partire da iOS v1.4.43. Per determinare se i sottotitoli non codificati sono disponibili per una specifica `PTMediaPlayerItem`, esamina `subtitlesOptions` proprietà di `PTMediaPlayerMediaItem`.

**Versione 1.4.42**

In questa versione non vengono aggiunte nuove funzioni. Per un elenco dei problemi risolti, vedi [Problemi risolti](#resolved-issues).

**Versione 1.4.41**

Modifiche API:

* **isSecure**: È stata introdotta una nuova API isSecure per impedire al lettore di registrare e generare un errore. Il valore predefinito è vero.

* **allowExternalRecording**: È stata introdotta una nuova API per consentire il mirroring di airplay per un contenuto protetto. Il mirroring dell&#39;airplay viene trattato come registrazione `allowExternalRecording` deve essere impostato su `True`, per consentire il mirroring dell&#39;airplay o impostare `False` per interrompere il mirroring dell&#39;airplay per contenuti sicuri. Per impostazione predefinita, `value` è vero.

**Versione 1.4.40**

Nessuna nuova funzionalità.

**Versione 1.4.39**

* iOS TVSDK è certificato con VHL 2.0.1 e con VHL 2.0.1 con Nielsen.

* iOS TVSDK viene aggiornato per effettuare richieste CRS dal nuovo host Akamai `primetime-a.akamaihd.net`.

* La nuova configurazione del nome host fornisce la distribuzione delle risorse CRS tramite HTTP e HTTPS (SSL) su larga scala.

**Versione 1.4.36**

Integrare e certificare VHL 2.0 in iOS TVSDK : Ridurre la barriera nel `VideoHeartbeatsLibrary` implementazione riducendo la complessità delle API.

**Versione 1.4.34**

**Informazioni sugli annunci in rete**

Le API TVSDK ora forniscono informazioni aggiuntive sulle risposte VAST di terze parti. Gli annunci ID, il sistema di annunci e le estensioni degli annunci VAST sono forniti in `PTNetworkAdInfo` classe accessibile tramite  `networkAdInfo`  su una Ad Asset. Queste informazioni possono essere utilizzate per l&#39;integrazione con altre piattaforme di Ad Analytics come **Analisi della moat**.

**Versione 1.4.31**

* **Metriche di fatturazione** Per soddisfare i clienti che desiderano pagare solo ciò che utilizzano, anziché un tasso fisso indipendentemente dall’uso effettivo, Adobe raccoglie le metriche di utilizzo e utilizza queste metriche per determinare quanto fatturare ai clienti.

   Ogni volta che TVSDK genera un evento di avvio del flusso, il lettore inizia a inviare periodicamente messaggi HTTP al sistema di fatturazione di Adobe. Il periodo, noto come durata fatturabile, può essere diverso per VOD standard, pro VOD (annunci mid-roll abilitati) e contenuti live. La durata predefinita di ciascun tipo di contenuto è di 30 minuti, ma il contratto con Adobe determina i valori effettivi.

* **Supporto multi-CDN per annunci CRS** TVSDK ora supporta Multi-CDN per gli annunci CRS. Fornendo i dettagli FTP per gli annunci CRS, puoi specificare posizioni CDN diverse da quelle di proprietà di Adobe predefinite, come [!DNL Akamai].

**Versione 1.4.29**

In `PTSDKConfig` la classe `forceHTTPS` È stata aggiunta l’API .

La `PTSDKConfig` class fornisce metodi per applicare SSL alle richieste effettuate a server Adobe Primetime ad decision ioning, DRM e Video Analytics. Per ulteriori informazioni, consulta la sezione `forceHTTPS` e `isForcingHTTPS` metodi di questa classe. Se un manifesto viene caricato su HTTPS, TVSDK conserva l&#39;uso del contenuto di HTTPS e rispetta tale uso quando carichi eventuali URL relativi da quel manifesto.

>[!NOTE]
>
>Le richieste a domini di terze parti come pixel di tracciamento annunci, URL di contenuti e annunci e richieste simili non vengono modificate ed è responsabilità dei fornitori di contenuti e dei server di annunci fornire URL supportati tramite HTTPS.

**Versione 1.4.18**

Primetime iOS TVSDK ora supporta le risorse JavaScript VPAID 2.0 per abilitare un’esperienza pubblicitaria interattiva ricca. Per ulteriori informazioni su VPAID 2.0, consulta Supporto di annunci VPAID .

**Versione 1.4.17**

* tvOS

   TVSDK supporta applicazioni native per tvOS.
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

>[!NOTE]
>
>Il modulo Nielsen è stato rimosso dalla build TVSDK, il TVSDK verrà aggiornato presto con un nuovo modulo di integrazione Nielsen.

**Ad Fallback, catena margherita nella logica di selezione degli annunci (Zendesk #3103)**

Per gli annunci VAST (creativi) con la regola di fallback abilitata, TVSDK tratta un annuncio con un tipo MIME non valido come un annuncio vuoto e tenta di utilizzare al suo posto gli annunci di fallback. Puoi configurare alcuni aspetti del comportamento di fallback. Per ulteriori informazioni, consulta Fallback di annunci per annunci VAST e VMAP.

**Versione 1.4.9**

**Segnalazione Di Sospensione Con Sostituzione Di Contenuti Alternativi**

Come parte dell’aggiornamento 1.4 TVSDK, Adobe ora supporta anche l’accesso e il ritorno dai blackout regionali rispetto ai contenuti lineari. Il TVSDK può ora elaborare due file manifest in parallelo, principale e alternativo, per monitorare i segnali di blackout anche quando viene mostrata una programmazione alternativa al posto della programmazione originale.

**Versione 1.4.8**

**Video Heartbeat Library (VHL) aggiornato alla versione 1.5**

* Possibilità di inviare metadati con inizio video o inizio video/annuncio/capitolo come dati contestuali.

* Meno traffico di rete - Gli heartbeat sono in media meno e le dimensioni sono più piccole.

**Versione 1.4.7**

* **Supporto per l’individuazione locale**

Supporto per le installazioni on-premise di Adobe Individualization Server per personalizzare la richiesta di individualizzazione del client per passare a un endpoint diverso.

* **Protezione dell&#39;uscita basata su risoluzione**

I criteri DRM ora possono specificare la risoluzione più elevata consentita, a seconda delle funzionalità di protezione dell&#39;output del dispositivo. Ad esempio: _Se è disponibile l&#39;HDCP, è possibile riprodurre contenuti con una risoluzione fino a 1080p; se l&#39;HDCP non è disponibile, è possibile riprodurre contenuti con una risoluzione fino a 480p._

**Versione 1.4.4**

* **Aggiornamento della Video Heartbeat Library (VHL) alla versione 1.4.1.1**

   * Aggiunta la possibilità di raggruppare diversi casi d’uso di analytics, da altri SDK o lettori, con Adobe Analytics Video Essentials.
   * Il tracciamento degli annunci è stato ottimizzato rimuovendo il `trackAdBreakStart` e `trackAdBreakComplete` metodi. L’interruzione pubblicitaria è dedotta dalla variabile `trackAdStart` e `trackAdComplete` chiamate ai metodi.
   * La `playhead` non è più necessario per il tracciamento degli annunci.
   * È stato aggiunto il supporto per il servizio Experience Cloud ID.

* **Integrazione SDK Nielsen**

Il TVSDK ora supporta l’invio di beacon mTVR e MDPR ID3 all’SDK Nielsen senza alcuna integrazione personalizzata. Per iniziare, scarica il 3.1.2.19 Nielsen iOS App SDK e segui le istruzioni riportate qui nella Guida per i programmatori di iOS.

**Versione 1.4.0**

* **Segnalazione Di Sospensione Con Sostituzione Di Contenuti Alternativi**

Come parte dell’aggiornamento 1.4 TVSDK, TVSDK ora supporta anche l’accesso e la restituzione dai blackout regionali rispetto ai contenuti lineari. Il TVSDK può ora elaborare due file manifest in parallelo, principale e alternativo, per monitorare i segnali di blackout anche quando viene mostrata una programmazione alternativa al posto della programmazione originale.

* **Rimuovi/sostituisci annunci C3**

Ora, non è necessario alcun lavoro di preparazione aggiuntivo per inserire dinamicamente nuovi annunci nelle risorse VOD (Video-on-demand) che escono dalla finestra C3. Il TVSDK fornisce ora un’API per rimuovere intervalli di contenuto personalizzati e inserire nuovi annunci in modo dinamico. Questa nuova potente funzionalità è utile anche nei casi in cui i contenuti live/lineari vengono trasmessi durante la trasmissione e vengono immediatamente ritirati per essere utilizzati come contenuti on-demand senza il tempo necessario per pulire la risorsa.

## Problemi risolti {#resolved-issues}

Se la risoluzione è associata a un problema segnalato, viene visualizzato un riferimento Zendesk, ad esempio ZD#xxxxx.

<!-- 

Comment Type: draft

 <p>All TVSDK customers who use CRS are strongly encouraged to upgrade to TVSDK 1.4.39 or latest on iOS and Android. This upgrade is a drop-in replacement to the existing app implementation. After the upgrade, check for the CRS creative URL requests in a proxy tool (for example, Charles) to verify that the version in the path reflects version 3.1. For example:</p> 
 <p><span class="code">https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/ 167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784bf3586d.m3u8</span></p> 

-->

<!--
Comment Type: draft

 <p>TVSDK versions earlier than version 1.4.28 sometimes exhibit a long delay in the startup time when ad-enabled content is played on devices that are running on iOS 10. To resolve this issue, upgrade to version 1.4.28 or later. Version 1.4.28 was released on August 31, 2016, and iOS 10 was released on September 13, 2016.</p> 
-->

**iOS TVSDK 3.13**

* (ZD 42085) - Problemi di riproduzione su flussi CMAF.

* (ZD-43215) - Arresto anomalo quando il lettore viene rifiutato mentre un annuncio è in corso.

* (ZD 43210) - La riproduzione iOS HLS si blocca quando il sottotitolo WebVTT è abilitato.

**iOS TVSDK 3.12**

* Lo streaming live non riesce dopo 15 minuti di riproduzione quando si utilizza TVSDK per iOS 3.10.

### Problemi risolti nelle versioni precedenti {#resolved-issues-previous}

**iOS TVSDK 3.11**

* (ZD#40998) - Il `isFallbackOnInvalidCreativeEnabled` causa l&#39;arresto anomalo dell&#39;applicazione.

* (ZD#41289) - `NSInvalidArgumentException` è osservato con il metodo `customParams` che porta all&#39;arresto anomalo dell&#39;applicazione.

**iOS TVSDK 3.10**

(ZD#40943) - Il lettore TVSDK non si attiva `PTMediaPlayerStatusError` notifica quando la rete non è disponibile.

**iOS TVSDK 3.9**

(ZD#40272) - iOS TVSDK non riproduce i sottotitoli VTT con errore 101001 e porta al blocco delle app.

**iOS TVSDK 3.8**

* (ZD#40087) - iOS si blocca con l’errore del lettore per il contenuto VOD scaduto.

* (ZD#40083) - Gli annunci pre-roll non vengono riprodotti per livestream con `OpportunityGenerator` e il lettore restituisce un errore.

* (ZD#39828) - `CurrentItem` manca l&#39;annotazione di nullità, causando l&#39;arresto anomalo del lettore quando lo stato del lettore contenuto nella notifica è `PTMediaPlayerStatusStopped`.

**iOS TVSDK 3.7**

(ZD#38961) - Il contenuto non viene riprodotto nella finestra Picture-in-Picture (PiP) dopo che un contenuto ha completato la riproduzione, quando più contenuti sono configurati per essere riprodotti nel PiP.

**iOS TVSDK 3.6**

Nessun nuovo problema in questa versione.

**iOS TVSDK 3.5**

Nessun nuovo problema in questa versione.

**Versione 3.3**

(ZD#37820) - Aggiunta dell’elenco Consentiti per l’intestazione personalizzata HS-Id, HS-SSAI-TAG.

**Versione 3.2**

* **Biglietto n. 36588** - Si osserva un arresto anomalo del lettore quando si chiama il metodo MediaPlayer STOP.

È stato corretto un arresto anomalo intermittente osservato quando si richiama il metodo STOP per alcuni flussi con sottotitoli.

* **Biglietto n. 37080** - Richieste duplicate visualizzate per chiamate Manifest.
Sono state corrette le richieste duplicate effettuate per gli URL Manifest durante la riproduzione. TVSDK effettua ora una chiamata per manifesto.

* **Biglietto n. 37** - La regola di normalizzazione CRS non riesce con il tipo di corrispondenza eq È stato corretto un caso in cui il lettore si arresta in modo anomalo quando viene rilevato l’ultimo set di regole di normalizzazione per i nomi host con un tipo di corrispondenza &quot;eq&quot;.

**Versione 3.1**

**Biglietto #36313** - Risultati intermittenti imprevedibili durante le interruzioni lineari degli annunci Riproduzione intermittente fissa durante le interruzioni lineari degli annunci nel flusso live.

**Versione 3.0.1**

**Biglietto36948** - CRS - Ordine di selezione delle risorse incoerente su iOS 12 La risorsa selezionata per CRS non è sempre la variante di qualità più elevata restituita in una risposta VAST o VMAP.

**Versione 3.0**

* **Biglietto35311** - Lo stato del lettore non si interrompe durante un&#39;interruzione della chiamata telefonica Aggiunto gestore di interrupt per impedire l&#39;interruzione del lettore. Al momento dell&#39;interruzione, lo stato del lettore diventa PAUSED e quindi riprende la riproduzione facendo clic sul pulsante di riproduzione.

* **Biglietto36685** - Live assets: viene calcolata una mancata corrispondenza tra il tempo e l’avanzamento del lettore e il tempo del marcatore SCTE. Il tempo corretto viene calcolato per i marcatori SCTE che sono in anticipo rispetto al punto live.

* **Biglietto36492** - `currentTime` e `localTime` non sono aggiornati quando si cerca una nuova posizione durante lo stato in pausa Il tempo corrente del lettore può ora essere impostato su zero nel caso in cui il lettore sia in stato di pausa; prima l&#39;ora corrente era impostata a zero solo in stato di riproduzione.

**Versione 1.4.45**

* **Biglietto36294** - iOS TVSDK non funzionante con Xcode 10 Sono stati risolti i problemi di compilazione con TVSDK su XCode 10. A causa dei dieci requisiti XCode, le app create su TVSDK per iOS 1.4.45 e versioni successive richiedono un target di distribuzione minimo come iOS 7.0

* **Biglietto36321** - Discrepanza osservata nell&#39;intervallo ricercabile tra `PTMediaPlayer` e `AVPlayer` istanza in _Riproduzione_ stato.

* **Biglietto36493** - `libstdc++` supporto su iOS 12 Sono stati risolti i problemi di compilazione con TVSDK su iOS 12. Le app basate su TVSDK per iOS 1.4.45 e versioni successive richiedono una destinazione di distribuzione minima come iOS 7.0

**Versione 1.4.44**

* **Biglietto34683** - Il Tempo Di Avanzamento Della Riproduzione Degli Annunci Va In Modo Negativo

Controlli aggiuntivi inseriti per gestire il caso in caso di mancata corrispondenza tra la durata segnalata dal server di annunci e il contenuto effettivo dell’annuncio.

* **Biglietto34801** - `currentTime` e `localTime` non venivano aggiornati quando si cercava una nuova posizione durante lo stato in pausa, ora il tempo corrente del lettore può essere impostato su zero nel caso in cui il lettore sia in stato di pausa; prima l&#39;ora corrente era impostata a zero solo in stato di riproduzione.

* **Biglietto35037** - Riproduci le bancarelle con URL errato quando si torna dall&#39;inserimento di annunci basato su segnali.
Correzione migliorata fornita per il problema chiuso #34385 nella versione 1.4.42. È stato aggiunto il codice di controllo e gestione delle eccezioni isCancelled per rendere più robusta la coda delle operazioni.

**Versione 1.4.43**

* (ZD#32990) - iOS: Riproduzione dei contenuti invece degli annunci su alcuni punti di cue. `selectedMediaOptionInMediaSelectionGroup` L&#39;API che faceva parte dell&#39;interfaccia AVPlayerItem ora è stata spostata in `AVMediaSelection` in iOS 11. Il problema è stato risolto utilizzando questa nuova API.

* (ZD#33683) TVSDK rimosso `==` suffisso dalle stringhe di metadati. Il problema è risolto nella logica di analisi.

* (ZD#33905) - iOS TVSDK che effettua chiamate ai file manifest con due agenti utente. Il problema dell’agente utente è stato risolto nella prima chiamata m3u8 (nuovo caso di installazione). I M3u8 hanno gli stessi agenti utente per tutte le chiamate ora.

* (ZD#34293) - I pre-rotoli inseriti sui flussi LINEAR non vengono riprodotti correttamente su iOS11. Il problema è stato risolto per gli annunci pre-roll.

* (ZD#34684) - Quando si applica il criterio di salto annunci, i fotogrammi degli annunci pre-roll vengono visualizzati per alcuni secondi. Una nuova API, `enableVodPreroll` è stato introdotto per disabilitare la riproduzione pre-roll nella riproduzione del vod. Il valore predefinito per questa API è _Sì_. L’API garantisce che le unioni di contenuti degli annunci vengano saltate nel contenuto principale.

* (ZD#34765) - Dopo aver chiamato `stop()`, vengono ancora scaricati alcuni segmenti di Transport Streams. Miglioramento della `Stop()` API per evitare il download dei segmenti aggiuntivi.

* (ZD#34865) - Annunci pre-scorrimento per [!DNL Livestream] vengono troncati su iOS. In merito ad iOS11 e all’aggiunta di un controllo aggiuntivo per verificare se il flusso è pre-roll o contenuto principale, viene risolto questo problema.

* (ZD#35093) - È stato corretto uno scenario di failover in cui, se la variante primaria del flusso non riesce all&#39;avvio (restituisce 404), la riproduzione non passa al flusso di backup.

**1.4.42 (1.4.42.118)**

* (ZD#34385) - La riproduzione termina con un URL errato quando si torna dall&#39;inserimento di annunci basati su segnali.

   Aumenta i conteggi simultanei massimi per `CustomAVAssetLoaderOperations`, in modo che le letture del manifesto possano continuare a essere eseguite.

* (ZD#34373) - Gli utenti finali non possono effettuare lo streaming su dispositivi collegati HDMI, quando la registrazione dello streaming non è consentita.

* (ZD#32678) - TVSDK non raccoglie gli ID annunci corretti su iOS.

   L’ID dell’annuncio finale viene ora rilevato nei ping VHL se sono presenti reindirizzamenti VAST/VMAP.

* (ZD#33904) - TVSDK non è registrato per le notifiche AVFfoundation `AVAudioSessionMediaServicesWereLostNotification` e `AVAudioSessionMediaServicesWereResetNotification`.

   `PTMediaServicesWereLostNotification` e `PTMediaServicesWereResetNotification` ora può essere registrato sull’app del lettore per ricevere le notifiche quando i servizi Media vengono reimpostati o persi.

* (ZD#33815) - I clienti non possono aggiornare le regole CRS per la priorità e la normalizzazione senza richiedere un aggiornamento dell’app.

   È stato aggiunto il `getCRSRulesJsonURL` e `setCRSRulesJsonURL` API di iOS TVSDK .

**Versione 1.4.41 (1.4.41.76)**

* (ZD #34464) - Problemi nella creazione dell&#39;app di riferimento con la versione 1.4.41 di TVSDK

   A partire da questa versione, è necessario Xcode 9 per compilare TVSDK per iOS.
* (ZD #29456) - L&#39;aria comincia in stato di pausa

   È stato risolto il problema di pausa che si verificava durante l’immissione di video in pausa durante l’immissione di Airplay.
* (ZD #30371) - L&#39;ora di inizio di AdBreak cambia quando inseriamo più di due annunci nel flusso lineare

   È stato corretto l’errore che impediva la riproduzione completa del contenuto su Apple TV durante il tentativo di riproduzione
* (ZD #32146)- No `PTMediaPlayerStatusError` viene ricevuto per contenuti HLS Live al blocco della versione beta di iOS 11 dev

   No `PTMediaPlayerStatusError` viene ricevuto per contenuti HLS Live e VOD sul blocco tramite Charles (Drop connection e 403).

* (ZD #29242) - La riproduzione video di Airplay non riesce con gli annunci abilitati.

   Quando gli annunci sono abilitati e AirPlay è abilitato all’avvio della riproduzione di un video, la riproduzione del video non viene mai avviata e non viene visualizzato alcun errore.

* (ZD#33341) - `DRMInterface.h` attiva gli avvisi di creazione in Xcode 9.

   Sono stati corretti due prototipi a blocchi in `DRMInterface.h` che mancavano la parola &quot;void&quot; negli elenchi dei relativi parametri.

* (ZD#31979) - Non viene compilato/eseguito quando è iOS 10 o versione successiva per iPhone 7/iPhone7+.

   È stato corretto il problema a causa del quale la compilazione di documenti IB per versioni precedenti ad iOS 7 non era più supportata.

* (ZD#32920) - Schermo vuoto all’interno di un’interruzione annuncio e senza completamento di un’interruzione annuncio.

   Quando un’interruzione annuncio presenta istanze di annunci e al termine di un’istanza di annunci, viene visualizzata una schermata vuota.

* (ZD#32509) - Disabilita la registrazione dello schermo iOS 11 Disabilita la registrazione dello schermo su iOS 11.

* (ZD#33179) - Errore di evento intermittente su iOS11.

   È stato corretto l’errore di evento in iOS 11.

**Versione 1.4.40** (1.4.40.72)

* (ZD #32465) - Impossibile gestire le playlist unite.

   Chiamata `finishLoadingWithError`(con: Errore) per la fondazione AV per provare flussi alternativi/attivare il failover.

* (ZD #31951) - Errore TVSDK durante le rotazioni della licenza.

   È stato risolto il problema di rotazione della licenza.
* (ZD #31951) - Schermo vuoto in un’interruzione annuncio e nessun completamento dell’interruzione annuncio.

   È stato risolto un problema a causa del quale gli annunci VPAID di Facebook restituivano spesso più blocchi CDATA in un unico `<AdParameters>` Nodo VAST.
* (ZD #33336) - iOS TVSDK - I pod di annunci non vengono riempiti, nonostante la quantità di annunci restituiti da FreeWheel.

   È stata creata una relazione padre-figlio tra l’annuncio di sequenza e l’annuncio di fallback e l’ordinamento in base alla sequenza e all’indice padre.

**Versione 1.4.39** (1.4.39.43)

* (ZD #32178) - La versione TVSDK di iOS non è corretta.

   L&#39;output della versione TVSDK nei file di registro era 1.0.211. È stato corretto per l&#39;output della versione corretta.

* (ZD #32199) - Caricamento annuncio persistente - Il video non viene visualizzato per il contenuto.

   La timeline di Adbreak locale che non veniva inizializzata in precedenza viene aggiornata prima dell’utilizzo.

* (ZD #27528) - Video, audio o entrambi si bloccano da 1 a 45 secondi dopo l’avvio della riproduzione di una risorsa, se l’audio secondario è impostato su non predefinito su iOS 1.2.

   Preparare e informare le tracce audio in stato Ready.

* (ZD #30411) - Se scegli una lingua secondaria Sap, potresti ottenere risultati inattesi, ad esempio nessun audio o audio errato.

   Preparare e informare le tracce audio in stato Ready.

* (ZD #32199) - Caricamento annuncio persistente - Il video non viene visualizzato per il contenuto.

   La timeline di Adbreak locale che non veniva inizializzata in precedenza viene aggiornata prima dell’utilizzo.

* (ZD #27528) - Video, audio o entrambi si bloccano da 1 a 45 secondi dopo l’avvio della riproduzione di una risorsa, se l’audio secondario è impostato su non predefinito su iOS 1.2.

   Preparare e informare le tracce audio in stato Ready.

* (ZD #30411) - Se scegli una lingua secondaria Sap, potresti ottenere risultati inattesi, ad esempio nessun audio o audio errato.

   Preparare e informare le tracce audio in stato Ready.

**Versione 1.4.38** (1.4.38.860)

* (ZD #29281) - iOS: Aggiungere AdSystem e ID creativo alle richieste CRS

Utilizzo di creative Id e AdSystem nella richiesta CRS in base alle regole di normalizzazione CRS

* (ZD #29176) - Crash on `PTAdPolicyDeligate` `satAdBreakAsWatched:position`

L&#39;arresto anomalo dovuto ad AdBreak vuoto viene gestito ora.

* (ZD #30125) - Gli annunci programmatici non funzionano nella piattaforma iOS

È stato aggiunto il supporto per gli annunci programmatici in iOS.

* (ZD #30782) - #EXT-X-PROGRAM-DATE-TIME Notification

L&#39;evento di metadati temporizzati non viene attivato per il tag # EXT-X-PROGRAM-DATE-TIME con flussi DRM LIVE.

**Versione 1.4.37 (1.4.37.842)**

* (ZD #28950 ) - Problema di riproduzione VOD

Problema di riproduzione quando il tag # EXT-X-PLAYLIST-TYPE nel flusso è impostato su Evento anziché su VOD

* (ZD #29281) - iOS: Aggiungere AdSystem e ID creativo alle richieste CRS

Utilizzo di Creative Id e AdSystem nelle richieste CRS in base alle regole di normalizzazione CRS.

* (ZD #29462) - Annuncio TremorHub in A&amp;E VOD che causa un arresto anomalo nelle app iOS

**Versione 1.4.36 (1.4.36.835)**

* (ZD #29418) - I cue con durata 0 (#EXT-X-CUE-OUT:0.000) causano l’arresto o l’arresto della riproduzione in iOS TVSDK.

Il problema è risolto e la riproduzione viene avviata correttamente.

* (ZD #29462) - L’aggiunta in VOD causa un arresto anomalo su iOS TVSDK .

Il problema è stato risolto. iOS TVSDK sta creando un `exception(AUDNetworkAdInfo::initWithAdId)` e non gestirlo. L&#39;eccezione è dovuta a un ID annuncio vuoto.

* (ZD #29281) - Aggiungi AdSystem e Creative ID alle richieste CRS.

Includi AdSystem e CreativeId come nuovi parametri nelle richieste 1401 e 1403 (tutti gli altri parametri rimangono gli stessi).

**Versione 1.4.35** (1.4.35.830)

* (ZD #27830) - È necessario determinare a livello di programmazione la differenza tra sottotitoli e sottotitoli in iOS.

TVSDK espone ora i due tipi che possono essere utilizzati per filtrare il tipo di didascalia richiesto.

* (ZD #29160) - I suggerimenti per gli annunci EXT-X-CUE-OUT non sono inseriti correttamente in TVSDK iOS.

Con EXT-X-CUE-OUT midroll annuncio è in esecuzione ora.

* (ZD #29100) - L’app subisce un arresto anomalo quando l’utente passa alla fine di un filmato.

Sono stati corretti più arresti anomali relativi alla sincronizzazione.

* (ZD #28785), (ZD #27712) e (ZD #25076) - L’app iOS si blocca durante i grandi eventi live.

Sono stati corretti più arresti anomali relativi alla sincronizzazione.

**Versione 1.4.34** (1.4.34.815 per iOS 6.0+)

* (ZD #28481) - Interruzione FER a causa dell&#39;aggiunta della chiave errata alla fine di un&#39;interruzione pubblicitaria per questi flussi FER

Per un flusso FER, la chiave prima dell’interruzione pubblicitaria viene inserita dopo la fine dell’interruzione pubblicitaria. Questo problema è stato risolto aggiungendo il *ultima chiave vista* alla fine della pausa pubblicitaria.

**Versione 1.4.33** (1.4.33.803 per iOS 6.0+)

* (ZD# 21701) Abilitare CRS per i sotto-conti

Abilitato inviando l’URL creativo originale per la richiesta CRS 1401 invece dell’URL normalizzato, come da requisito per il back-end CRS.

* (ZD# 26218) - `PSDKResources.bundle` problema di caricamento

Questo problema è stato risolto aggiornando il caricamento delle risorse per cercare da tutti i bundle disponibili.

* (ZD# 27460) Prima chiamata ad Midroll: POST a `cdn.auditude.com` che restituisce 403.

Il nuovo account CDN non è in grado di gestire una richiesta CDN di POST. Questo problema è stato risolto aggiornando il codice per rendere il `cdn.auditude.com` richiesta di essere GET invece di POST.

**Versione 1.4.32** (1.4.32.792 per iOS 6.0+)

* (ZD# 27132) Supporto dei valori decimali per VMAP Ad Breaks.

Quando il contenuto non era segmentato lungo le interruzioni pubblicitarie definite, i numeri interi causavano posizionamenti imprevisti degli annunci. Il problema è stato risolto non convertendo i valori decimali in numeri interi.

* (ZD# 27189) Il contenuto AES con il tag EXT-X-DISCONTINUITY-SEQUENCE non viene riprodotto correttamente.

Il problema è stato risolto inserendo il tag all&#39;inizio della playlist.

**Versione 1.4.31** (1.4.31.785 per iOS 6.0+)

* (ZD# 24528) Implementa le metriche di utilizzo TVSDK per la fatturazione

Per ulteriori informazioni, consulta [Metriche di fatturazione].

* (ZD# 24642) Supporto Picture-in-Picture per TVSDK

La funzione picture-in-picture, che talvolta non funzionava correttamente, è stata corretta.

* (ZD# 25246) Segnali di interruzione annunci errati

Questo problema è stato risolto allineando i tag di discontinuità tra i vari manifesti.

* (ZD# 26218) Il processo di compilazione dell&#39;applicazione si complica quando si tenta di includere `PSDKLibrary.framework` nel framework applicativo del cliente

Questo problema è stato risolto impacchettando il `PSDKLibrary.framework` come richiesto.

* (ZD# 26364) Supporto multi-CDN per annunci CRS

Per ulteriori informazioni, consulta Supporto di più CDN per CRS Ad Delivery.

* (ZD# 27028) Ritardo nella riproduzione di alcuni flussi in iOS 10.

Questo problema è stato risolto fornendo una soluzione per i flussi che non hanno un&#39;estensione M3U8.

**Versione 1.4.30** (1.4.30.754 per iOS 6.0+)

In questa versione sono stati risolti i seguenti problemi per TVSDK:

* (ZD# 24180) Aggiungi un&#39;intestazione personalizzata inserì nell&#39;elenco Consentiti.

È stata aggiunta una nuova intestazione personalizzata all’inserire nell&#39;elenco Consentiti TVSDK.

* (ZD# 25016) Il flusso di failover viene selezionato in modo casuale quando vengono impostati i parametri di controllo ABR

Questo problema è stato risolto mantenendo i flussi ABR in ordine quando vengono fornite le impostazioni ABR con `initialBitrate` in un flusso che include gli URL di failover. In questo modo si evita la riproduzione dei flussi di failover anziché del flusso primario.

* (ZD# 25076) Arresto anomalo su `PTAuditudeAdResolver loadComplete`

È stato risolto il problema che si verificava durante l&#39;avvio/arresto rapido di più istanze PTMediaPlayer con annunci.

* (ZD# 25960) Nessuna tara aggiuntiva per i tag sottoscritti che attiva la trasmissione della notifica della modifica dei metadati

Il problema per cui un tag di sottoscrizione non viene notificato quando viene visualizzato prima che il primo segmento nel manifesto sia stato risolto.

* (ZD# 26084) PSDK lancio di un 106000.101000.Errore del decodificatore -11833 durante la transizione dall&#39;ultimo annuncio al contenuto di intrattenimento

Quando l’ultimo tempo di inizio dell’interruzione pubblicitaria dal VMAP cade prima del completamento della durata totale, in determinate condizioni la chiave non viene inserita fino a dopo la fine dell’ultima interruzione pubblicitaria. Questo problema è stato risolto.

* La libreria Video Heartbeat (VHL) è stata aggiornata alla versione 1.5.9 per risolvere i seguenti problemi:

* (ZD #22351) VHL - Analytics: Durata della risorsa video live

Questo problema è stato risolto aggiungendo il  `assetDuration`  API a `PTVideoAnalyticsTrackingMetadata` per aggiornare la durata della risorsa per i flussi live/lineari e fornire una logica per il controllo del flusso live.

* (ZD# 22675) VHL - Analytics: Aggiornamento della durata della risorsa video in tempo reale

Questo problema è lo stesso di ZD #22351.

* (ZD #25908) VHL - Analytics: Adobe Heartbeat Event Crash

Questo problema è stato risolto aggiornando l’implementazione per utilizzare l’ultima versione di VHL per iOS versione 1.5.9 per migliorare la stabilità e le prestazioni.

* (ZD #25956) VHL - Analytics: Arresto anomalo durante la riproduzione ripetuta dei video

Questo problema è lo stesso di ZD #25908.

**Versione 1.4.29** (1.4.29.743)

* (ZD# 23901) Gli annunci di terze parti non vengono riprodotti

Questo problema è stato risolto passando alla struttura URL CRS v3 per includere l&#39;ID di zona nell&#39;URL reinserito.

* (ZD #25183) Problemi di riproduzione DRM su tvOS e iOS

Questo problema è stato risolto fornendo il supporto per più tag chiave necessari per il supporto multi-DRM.

* (ZD# 25334) TVSDK non riesce a riprodurre un contenuto condiviso cDVR

Questo problema è stato risolto impedendo a TVSDK di convertire stringhe vuote in URL assoluti.

* (ZD# 25347) Imposta intestazione HTTP personalizzata su AVURLAsset

Supporto per intestazioni personalizzate sulle richieste di segmenti tramite `PTNetworkConfiguration` Classe aggiunta.

**Versione 1.4.28** (1.4.28.722)

* (ZD #24549) Chiamate multiple per il tracciamento degli annunci

Questo problema è stato risolto aggiornando il gestore della timeline per ascoltare le notifiche su un oggetto specifico quando vengono creati più lettori.

* (ZD #24758) `PTManifestLogger` non supporta iOS 8

Questo problema è stato risolto aggiornando la libreria di utilità logger alla destinazione di distribuzione della versione 7.0.

* (ZD #24775) Flusso ritardato dovuto agli annunci

Questo problema è stato risolto calcolando correttamente la deriva della durata nelle playlist degli eventi.

* (ZD #24799) Alcuni episodi non vengono riprodotti su iOS APP

Questo problema è stato risolto utilizzando il server web locale per i sottotitoli quando i file WebVTT sono soggetti a restrizioni geografiche.

**Versione 1.4.27** (1.4.27.711) per iOS 6.0+

* (ZD #24089) - Ottimizzazioni per la risoluzione degli annunci su flussi DVR lunghi

Questo problema è stato risolto aggiungendo più ottimizzazioni per ridurre il tempo necessario per elaborare la finestra DVR in flussi live/lineari.

* (ZD #21554) - I beacon di errore TVSDK non vengono attivati per `application-type = video/mp4`

Questo problema è stato risolto abilitando il lettore a ping degli URL di tracciamento degli errori corretti su formati di risorse non validi.

* (ZD #24424) - Arresto anomalo del tipo `EXC_BAD_ACCESS KERN_INVALID_ADDRESS` è originario dell&#39;interno `PSDKLib` per iOS su dispositivi hardware più recenti.

È stato corretto l’arresto anomalo che si verificava a causa di un’istanza del lettore multimediale non allocata, quando la riproduzione viene scambiata rapidamente tra flussi diversi.

* (ZD #24575) - Arresto anomalo in TVSDK su dispositivi a 32 bit quando `enableDebugLog=true`

È stato risolto il problema nel formato di registro che causava l’arresto anomalo sui dispositivi a 32 bit quando la registrazione è abilitata.

**Versione 1.4.26** (1.4.26.702) per iOS 6.0+

* (ZD# 20213) - TVSDK FW deve essere dinamico/modularizzato per XCode7

Risolto aggiornando le librerie con il supporto del modulo .

**Versione 1.4.25** (1.4.25.684) per iOS 6.0+

* (ZD #19629) - Pausa video in tempo reale durante l&#39;ingresso di Airplay a ATV 4

Questo problema è stato risolto aggiungendo un periodo di attesa dopo aver rimosso gli elementi obsoleti ma prima di aggiungere nuovi elementi al `AVQueuePlayer`. Senza il periodo di attesa, le notifiche vengono inviate all’elemento errato.

* (ZD #19856) - Non viene visualizzato alcun sottotitolo se attivato per impostazione predefinita

Sono stati risolti i problemi relativi alla playlist del webvtt, che causava la visualizzazione errata dei sottotitoli.

* (ZD #21590) - Prestazioni e tracciamento video nelle build di origine più recenti

Il problema relativo alla lunghezza del video mancante in `VideoAnalytics` è stato corretto.

* (ZD #20202) - L’impostazione dello stile dei sottotitoli personalizzati arresta l’app iOS

Questo problema è stato risolto aggiungendo ulteriori controlli oggetti nulli durante l’impostazione degli stili dei sottotitoli.

* (ZD #20709) - La lunghezza del video indicata come 0 nel tracciamento dell’avvio del video

Questo problema è lo stesso di (ZD #21590).

* (ZD #22280) - Lunghezza video di Analytics impostata su 0

Questo problema è lo stesso di (ZD #21590).

* (ZD #22592) - Problemi con Airplay in Primetime

Questo problema è lo stesso di (ZD #19629).

* (ZD#22922) - Commutazione manuale del bitrate per iOS

Questo problema è stato risolto fornendo un&#39;opzione per specificare il bitrate massimo.

* (ZD #23084) - Conformità Apple per le reti solo IPv6

I simboli non consigliati da Apple per la compatibilità IPv6 sono stati rimossi.

**Versione 1.4.24** (1.4.24.661) per iOS 6.0+

* ZD #2548) - Supporto Primetime per la pubblicità interattiva su dispositivi mobili - VPAID 2.0

Questo problema è stato risolto aggiornando la logica per nascondere la visualizzazione del lettore se un annuncio VPAID non viene riprodotto.

* (ZD #20101) - L’implementazione del capitolo personalizzato attiva un evento di avvio del capitolo durante la riproduzione dell’annuncio

Questo problema è stato risolto aggiornando `VideoAnalyticsTracker` per rilevare correttamente l&#39;inizio/completamento del capitolo durante la transizione tra i limiti dei capitoli e non dei capitoli.

* (ZD #20784) - Analytics: Attivazione di contenuti completi per transizioni video in tempo reale

Questo problema è stato risolto aggiungendo una logica per attivare manualmente il completamento del contenuto durante una sessione di tracciamento video.

Sono state aggiornate le seguenti librerie:

* Libreria AdobeMobile alla versione 4.10.0
* Libreria VHL a 1.5.6
* Libreria VHL-Nielsen a 1.6.7
* (ZD #21855) - I sottotitoli non vengono riprodotti dopo il mid-roll

In questo problema, i tag di discontinuità duplicati causavano la mancata visualizzazione dei sottotitoli dopo il mid-roll. Questo problema è stato risolto rimuovendo i tag di discontinuità che si trovano l&#39;uno accanto all&#39;altro.

* (ZD #21994) - Stringa fuori limite in `PTHLSUtils`

La causa più probabile dell’arresto anomalo è quando un EXT-X-KEY ha un URL circondato da virgolette.

* ZD #22074) - `AUDVAST` Arresto anomalo che si verifica una volta al minuto su iOS

Nella versione 1.4.23, è stato corretto l’arresto anomalo causato dalla presenza di caratteri non sicuri in un URL di reindirizzamento VAST. Tuttavia, TVSDK continuava a saltare questi annunci.

Questo problema è stato risolto gestendo i caratteri non sicuri e consentendo la riproduzione degli annunci.

* (ZD #22694) - `PTMediaPlayer`.  Visualizzazione nascosta dal lettore

Questo problema è stato risolto aggiornando la logica per nascondere la visualizzazione del lettore se un annuncio VPAID non viene riprodotto.

**Versione 1.4.23** (1.4.23.641) per iOS 6.0+

* (ZD #18016) - Nessuna risposta da Primetime SDK con una condizione di rete errata

Questo problema è stato risolto migliorando la notifica di errore quando un errore irreversibile da `AVFoundation` si verifica e consente all&#39;app di gestire il riavvio dopo l&#39;errore.

* (ZD #20580) - Arresto anomalo in `PTSplicerManager`

Questo problema è stato risolto fornendo ulteriore protezione dai problemi di concorrenza che causano l&#39;arresto anomalo.

* (ZD #21782) - Codice di errore iOS 10100

È stato risolto il problema che causava la restituzione di un errore 101000 da parte del TVSDK durante l’avvio della riproduzione su flussi DRM di Adobe Access.

* (ZD #21889) - La riproduzione di annunci online e contenuti offline non riesce

È stato risolto il problema che causava un errore di riproduzione dopo la correzione di un annuncio su contenuto offline crittografato AES.

* (ZD #22074) - Arresto anomalo AUDVAST che si verifica una volta al minuto su iOS

Questo problema è stato risolto migliorando la gestione dei tag di annunci VAST di terze parti che contengono caratteri non validi nell&#39;URL.

* (ZD #22257) - Il TVSDK non riesce a riprodurre il flusso DRM

È stato risolto il problema che causava la restituzione di un errore 101000 durante l’avvio della riproduzione su flussi DRM di Adobe Access.

**Versione 1.4.22** (1.4.22.627) per iOS 6.0+

* (ZD #18709) - Arresto anomalo nel TVSDK per iOS

È stato risolto il problema relativo a un arresto anomalo che si verificava su alcuni flussi protetti da DRM di accesso Adobe.

* (ZD #18850) - Aggiorna la logica di selezione creativa in base alle regole CRS

Questo problema è stato risolto aggiungendo un file di configurazione .json per specificare la priorità di selezione creativa.

* (ZD #19770) - Il feed video AES protetto non viene più riprodotto

È stato risolto il problema relativo alla mancata riproduzione di alcuni flussi reindirizzati di 302.

* (ZD #19629) - Pausa video in tempo reale durante l&#39;ingresso di Airplay a ATV 4

Questo problema è stato risolto aggiungendo una soluzione per mettere in pausa i video in tempo reale quando la riproduzione airplay è attivata per i dispositivi Apple TV 4. Il problema sembra essere un problema di Apple TV 4.

* (ZD #21119) - Il TVSDK viene arrestato dopo la riproduzione dell&#39;annuncio

È stato aggiunto il supporto per i flussi crittografati AES con una sequenza IV durante l’utilizzo dell’inserimento di annunci.

* (ZD #21125) - Ritorno dall&#39;annuncio live/lineare all&#39;inizio

È stato aggiunto il supporto per tornare da un’interruzione pubblicitaria prima che l’interruzione pubblicitaria venga riprodotta fino al completamento. La restituzione anticipata è indicata tramite un tag manifest personalizzato.

* (ZD #21224) - Supporto di Airplay per flussi token provenienti da Akamai

Le API sono state aggiunte al `PTNetworkConfiguration` per aggiungere cookie come parametri URL ai segmenti per determinati flussi token Akamai.

* (ZD #21287) - Registro estraneo

È stato risolto un problema relativo ad alcune istruzioni di registro visualizzate per impostazione predefinita nella console xcode anche quando la registrazione è disabilitata.

* (ZD #21446) - Gli eventi Ad Break a volte non attivati dal TVSDK

Nei flussi EVENTO, le interruzioni pubblicitarie non vengono attivate correttamente nella build della versione precedente. Questa build risolve questo problema.

**Versione 1.4.21** (1.4.21.605) per iOS 6.0+

* (ZD #20749) - Fallback salta le risposte VAST non vuote; Gli URL di tracciamento degli annunci aggiuntivi vengono attivati

È stato risolto un problema relativo ai ping duplicati sugli annunci di fallback.

**Versione 1.4.20** (1.4.20.590) per iOS 6.0+

* (ZD #18639) - Il TVSDK utilizza CPU/risorse eccessive su una risorsa di registrazione a caldo lunga

L&#39;utilizzo eccessivo di CPU/risorse è stato corretto nei due livelli. In primo luogo, consentendo l&#39;esecuzione della funzione di aggiornamento del tempo su una coda globale, invece del thread principale, e ottimizzando l&#39;utilizzo della CPU per l&#39;analisi del manifesto con il m3u8 elaborato e memorizzato in cache in precedenza.

* (ZD #19349) - Gli annunci pre-roll vengono ignorati durante la limitazione della connessione di rete.

Questo problema è stato risolto fornendo un evento di timeout (requestTimeout) all&#39;applicazione e al `adMetadata.adRequestTimeout` API per ignorare il timeout predefinito di 10 secondi.

* (ZD #19446) - Notifica mancante sui flussi live

Questo problema è stato risolto consentendo all’applicazione di sottoscrivere `EXT-X-PROGRAM-DATE-TIME` sui flussi in diretta.

* (ZD #19459) - Arresto anomalo durante la preparazione dell&#39;audio alternativo con `PTMediaPlayerItem` `prepareAudioOptionsWithAVMediaSelectionOptions`
* (ZD #19460) - Crash - `[PTMediaPlayerItem prepareSubtitlesOptionsWithAVMediaSelectionOptions:nonForcedOptions:]`

Questo problema è lo stesso di Zendesk #19459.

* (ZD #19574) - Il TVSDK non restituisce i dati di risposta M3U8 per il contenuto DRM o non DRM

Nel caricamento iniziale del file manifesto in `PTMediaPlayerItem.prepareToPlay`, se il caricamento del manifesto non è riuscito, il TVSDK non segnala il corpo della risposta di errore all&#39;applicazione.

Questo problema è stato risolto consentendo al TVSDK di segnalare la risposta di errore come un errore all’applicazione.

* (ZD #19615) - La logica di fallback non funziona

Nell&#39;implementazione corrente, gli annunci di fallback sono stati saltati e non sono stati ricompilati a meno che questi annunci non siano in formato m3u8. Questo problema è stato risolto aggiungendo anche il supporto per il riconfezionamento degli annunci di fallback.

* (ZD #19770) - Il TVSDK non riproduce alcun contenuto AES protetto con reindirizzamento 302

Il problema di reindirizzamento è stato risolto perché l&#39;URL di reindirizzamento veniva eliminato da `cleanConnectionData` prima che possa essere utilizzato per analizzare il manifesto.

* (ZD #19856) - I sottotitoli non vengono visualizzati per alcuni bit rate quando sono attivati per impostazione predefinita

Questo problema è stato risolto gestendo l’errore da iOS per i segmenti dei flussi in cui i sottotitoli non vengono visualizzati.

* (ZD #19868) - Il TVSDK si blocca quando viene trafficato un creativo non valido

È stato corretto l’arresto anomalo del TVSDK che stava disallocando in modo errato un’istanza del parser esteso.

* (ZD #20180) - Gli annunci VPAID vengono saltati occasionalmente

Il tipo di mime JavaScript non veniva sempre incluso o considerato come un tipo di mime valido. Questo problema è stato risolto includendo JavaScript come tipo di MIME valido.

* (ZD #20749) - Fallback salta le risposte VAST non vuote; Gli URL di tracciamento degli annunci aggiuntivi vengono attivati

Il problema in cui alcuni dei creativi non vengono riconfezionati è stato risolto.

**Versione 1.4.19** (1.4.19.563) per iOS 6.0+

* ZD #18639) - Il TVSDK utilizza CPU/risorse eccessive su una lunga risorsa di registrazione a caldo

Questo problema è stato risolto ottimizzando la riscrittura della playlist DRM m3u8 ai bit della cache della playlist che sono stati riscritti in precedenza. Questo è più pertinente quando si riproducono flussi live m3u8 per i quali viene scaricato m3u8 dopo ogni download del segmento.

* (ZD#18956) - `player.drmManager` è nil quando il punto di interruzione è impostato in iOS Demo Player

Questo problema è stato risolto aggiornando il `PTMediaPlayer.drmManager` Implementazione API per riprendere DRMManager dal framework DRM.

**Versione 1.4.18** ( 1.4.18.557) per iOS 6.0+

* (ZD #18844) Tracciamento della testina di riproduzione per i contenuti live in iOS Player.

Questo problema è stato risolto consentendo alle applicazioni di impostare il proprio valore di playhead.

* (Zendesk #18518) - Se il nome del video non è specificato, il nome TVSDK viene impostato automaticamente su * lettore basato su PSDK.*

Questo problema è stato risolto rimuovendo il valore predefinito per il nome del lettore.

**Versione 1.4.17** (1.4.17.545) per iOS 6.0+

* (Zendesk #2228) - Migliorare il TVSDK per restituire la risposta JSON del recupero di un manifesto

Invece di inviare un errore quando il contenuto non è M3U8, il DRM Framework restituisce un valore DRMMetadata nil. Il problema è stato risolto aggiungendo metadati per esporre il contenuto quando si verifica la notifica M3U8_PARSER_ERROR.

* (Zendesk #2231) - Errore restituito dal recupero del manifesto non disponibile in MediaPlayerNotification

Stessa risoluzione di Zendesk #2228

* (Zendesk #3304) - VAST 3.0 `[ERRORCODE]` macro non compilata

Il problema in cui [!DNL Auditude] L&#39;SDK non riesce a inviare un ping quando l&#39;URL di tracciamento ha spazi all&#39;inizio è stato risolto.

* (Zendesk #17294) - Crash [!DNL SecKeyRawSign]

È stato risolto un possibile arresto anomalo quando il codice del cliente utilizza la catena di chiavi.

* (Zendesk #18008) - Cookie di supporto per iOS8+ per il supporto di flussi token

I flussi token di Akamai richiedono l’invio di cookie su richieste di segmenti e questo non era possibile su iOS 7 e versioni precedenti. A partire da iOS 8, Apple ha aggiunto un’API che consente di trasmettere i cookie per le richieste di segmenti. Questo supporto è ora disponibile nel TVSDK. È stato aggiunto anche il supporto per l’invio di un agente utente, se disponibile.

* (Zendesk #18166) - TVSDK 1.4.15 fornisce centinaia di avvisi durante la compilazione con `DWARF` con `dSYM` opzioni file

Tutti gli avvisi sono stati risolti.

**Nota**: Sono state aggiunte librerie compatibili con tvOS per TVSDK .

**Versione 1.4.16** (1.4.16.1454)

* Zendesk #3875 - Tab S Arresto anomalo durante la riproduzione

Ripristino della dipendenza di OKHTTP in corso [!DNL Auditude] per CRS perché TVSDK ora utilizza direttamente `httpurlconnection` invece di curl. Il problema è stato risolto cancellando le eccezioni prima di effettuare un&#39;altra chiamata JNI.

* (Zendesk #4487) - Tracciamento del canale lineare dei contenuti

Il problema è stato risolto inizializzando nuovamente il tracciatore heartbeat video durante una sessione di riproduzione del flusso lineare.

* (Zendesk #17919) - Android - la ricerca del contenuto causa un errore di battito cardiaco

Il problema era risolvere il battito cardiaco in uno stato di errore quando c&#39;è una ricerca in un capitolo

* (Zendesk #18053) - L&#39;applicazione che utilizza il TVSDK si blocca su Marshmallow

Il TVSDK si bloccava su Android™ M OS quando la libreria TVSDK utilizza un codice neon che esegue YUV `->` Conversione del colore in RGB. Questo problema è stato risolto aggiornando le funzioni che causano il problema utilizzando la versione non neon di `code`.

* (Zendesk #18072) - Android M - Arresto anomalo dell&#39;applicazione

Questo arresto anomalo si verifica durante la chiamata `MediaCodecList` e `MediaCodecInfo` API per verificare se il profilo e il livello sono supportati. Adobe sta cercando il supporto Google alla ricerca di ulteriori informazioni. Questo problema è stato risolto fornendo una soluzione temporanea caricando anticipatamente tutte le informazioni sul codec per evitare di chiamare queste API solo quando sono necessarie informazioni sul codec.

* (Zendesk #18074) - Sottotitoli arabi non funzionanti su Nexus con Android™ 6.0

Questo problema è stato risolto sostenendo la mappa dei font Android™ CTS.

**Versione 1.4.15** (1.4.15.512) per iOS 6.0+

**Nota**: Il modulo Nielsen è stato rimosso dalla build TVSDK, ma il TVSDK verrà aggiornato presto con un nuovo modulo di integrazione Nielsen.

* (ZD #2228) - Errore restituito dal recupero del manifesto non disponibile in `MediaPlayerNotification`

Sono stati aggiunti metadati per esporre il contenuto al momento della notifica `M3U8_PARSER_ERROR` si verifica.

* (ZD #4437) - Arresti anomali all&#39;interno dell&#39;SDK di Adobe Primetime

È stato corretto un arresto anomalo segnalato durante la preparazione di sottotitoli/audio alternativo.

* (ZD #4487) - Tracciamento del canale lineare dei contenuti

È consentita la riinizializzazione del tracciatore heartbeat video durante una sessione di riproduzione del flusso lineare.

**Versione 1.4.14** (1.4.14.498) per iOS 6.0+

* (ZD #17260) - Arresto anomalo su `playlistManagerForURL`

È stato corretto un arresto anomalo intermittente dovuto a problemi di concorrenza.

**Versione 1.4.13** (iOS 6.0+)

* (ZD #3304) - VAST 3.0 `[ERRORCODE]` macro non compilata

   * Il codice di errore 400 viene esposto se l’annuncio in linea presenta un contenuto creativo non valido.
   * `[ERRORCODE]` macro è codificata in URL.

* (ZD #3865) Integrazione Heartbeat con gli annunci IMA

È stato corretto un bug a causa del quale la lunghezza del video veniva riportata in modo errato.

* È stato aggiornato il lettore demo TVSDK per supportare iOS 9

Per supportare correttamente iOS 9, è necessario configurare le eccezioni di Application Transportation Security. Per la demo, l&#39;ATS è completamente disabilitato.

**Versione 1.4.12** (1.4.12.464) per iOS 6.0+

* (ZD #4521) Test CRS lato client e SSAI

È stato corretto MD5 invertito errato nell&#39;URL 3P.

**Versione 1.4.12** (1.4.12.463) per iOS 6.0+

* (ZD #2751) CSAI e CRS / Miglioramento: Gestisci gli elementi dinamici in determinati URL di file multimediali.

È stato aggiornato Creative Repackaging Service per gestire correttamente gli annunci con URL creativi dinamici.

* (ZD #3654) Perdita di memoria nella versione PSDK dopo 1.3.4.166

È stata corretta una perdita di memoria in `drmFramework` con riproduzione normale su dispositivi iOS 8.2

* (ZD #3988) Il preroll viene ignorato quando si cerca di nuovo in esso dopo la prima riproduzione

È stato corretto un bug che impediva la corretta disattivazione dei criteri degli annunci.

* (ZD #4017) Richiesta dell’API iOS per forzare la riproduzione degli annunci nella ricerca all’indietro

Risolto con correzione per ZD #4279

* (ZD #4279) HLS TVSDK ad Insert -302 problema di reindirizzamento su iOS e Desktop

È stato corretto un bug a causa del quale una risorsa pubblicitaria utilizzava un URL di reindirizzamento relativo

**Versione 1.4.9** (1.4.9.427) per iOS 6.0+

* (ZD #3075) Problema di raggiungibilità di Internet - iOS

È stata aggiunta una notifica per rilevare quando la riproduzione si è arrestata.

* (ZD #3193) Richiesta di modifica dell’API del profilo in TVSDK

Aggiornato `PTPlaybackInformation` per esporre il Bitrate aggiornato indicato. Aggiornato `BITRATE_CHANGE` notifica per essere più affidabile e preciso ai bit rate segnalati da M3U8.

* (ZD #3324) Problema di reporting degli annunci Primetime quando nessun supporto pubblicitario in VMAP

Supporto per il ping di URL vuoti di tracciamento delle interruzioni pubblicitarie, TVSDK ora verifica l’avvio dell’interruzione pubblicitaria e completa i ping per le interruzioni pubblicitarie vuote.

**Versione 1.4.8** (1.4.8.402)

* (ZD #3158) IOS 7 si blocca in Riproduzione eventi completa

**Versione 1.4.7** (1.4.7.382)

* (ZD #2197) Tracciamento degli errori degli annunci. Aggiunta notifica per la risorsa non riuscita a caricare il manifesto.
* (ZD #2894) Player Esegue quattro richieste manifest di livello superiore durante la riproduzione.
* (ZD #2992) [!DNL Auditude] Segnalazione di durate e identificatori strani.

**Versione 1.4.6**(1.4.6.325)

* (ZD #2197) Tracciamento degli errori degli annunci. Aggiunta notifica per la risorsa non riuscita a caricare il manifesto

**Versione 1.4.5** (1.4.5.283)

* (ZD #2141) Implementazione di Analytics per [!DNL TreeHouse] app, aggiunta `AdobeAnalyticsPlugin.a` libreria per creare il pacchetto .
* Aggiornamento della libreria Heartbeat video alla versione 1.4.1.2
* (PTPALY-4226) (relativo a ZD #2423) L&#39;esecuzione della reimpostazione DRM può comportare l&#39;eliminazione dei dati del documento dell&#39;applicazione.

**Versione 1.4.4** (1.4.4.242)

* Aggiornamento della Video Heartbeat Library (VHL) alla versione 1.4.1.

* (ZD #2435) Documentazione TV SDK sugli aggiornamenti delle esigenze di analisi

**Versione 1.4.2** (1.4.2.210 : iOS 6.0+)

* (ZD #1129) `_player.currentItem.audioOptions` reso vuoto
* (ZD #2109) Primetime PSDK 1.4.1.125 non funziona con Xcode 5.1.1
* (ZD #2137) Arresto anomalo in PSDK su iOS quando non è possibile caricare i metadati DRM

**Versione 1.4.1**(1.4.1.125)

* (ZD n. 1107) [!DNL CocoaLumberjack] simboli duplicati
* (ZD #1644) Modificare l’agente utente iOS per il targeting e il reporting
* (ZD #1850) File Lumberjack di cacao inclusi nell’SDK di iOS
* (ZD#1908) I tag personalizzati vengono ignorati da PSDK se sono presenti più di 1

**Versione 1.4.0** (1.4.0.32)

* Zendesk #1024 - Funzione per rimuovere l&#39;annuncio dal flusso tramite manifesto

## Certificazione e supporto dei dispositivi {#device-certification-and-support}

>[!NOTE]
>
>Le seguenti funzioni sono: **not** supportato in TVSDK :
>
>* Slow motion, su qualsiasi piattaforma o versione.
>* Giochi di trucco dal vivo.


**Versione 1.4.43**

* TVSDK 1.4.43 è certificato per iOS 11.

**Versione 1.4.29**

* TVSDK 1.4.29 è stato certificato per iOS 10.

**Versione 1.4.28**

* TVSDK 1.4.28 è stato certificato per iOS 10 Beta 7.
* Supporto DRM per forzare HTTPS aggiungendo  `forceHTTPS`  e `isForcingHTTPS` API.
* Sono state aggiornate le librerie VHL a 1.5.8, Adobe Mobile Libraries a 4.8.4 e la libreria di utilità logger alla destinazione di distribuzione della versione 7.0.

**Versione 1.4.19**

Questa versione del TVSDK è stata certificata con il supporto FairPlay per iOS e tvOS.

**Versione 1.4.17**

* tvOS

   Questa versione di TVSDK include il supporto per tvOS ed è stata certificata per flussi HLS non crittografati.

   **Nota**: Ricorda le seguenti linee guida per la compilazione:

   * Il supporto per tvOS TVSDK è limitato a flussi crittografati DRM non Adobi. È necessario rimuovere il riferimento a `drmNativeInterface.framework` nelle impostazioni della build tvOS. I flussi crittografati AES sono ancora supportati.
   * Apple richiede che tutte le applicazioni Apple TV siano abilitate per il bitcode, pertanto devi attivare questo flag nelle impostazioni del progetto.

## Problemi noti e limitazioni {#known-issues-and-limitations}

* A causa della deprecazione della classe UIWebView di iOS, in iOS TVSDK 3.6 e successivi:
   * Gli annunci VPAID non vengono riprodotti come previsto in iPad 13.
   * Gli annunci Companion non giocano come previsto.

* In iOS TVSDK, tutti gli annunci vengono inseriti nel manifesto del contenuto. I comportamenti degli annunci vengono implementati mediante ricerca in base alla durata dei contenuti e dei segmenti di annunci. Quindi, se le durate del segmento non sono precise, la ricerca potrebbe non terminare sempre con il fotogramma esatto dell&#39;inizio o della fine dell&#39;interruzione dell&#39;annuncio. Anche se le durate sono al frame, c&#39;è una tolleranza che la piattaforma stessa impone alla ricerca e ci possono essere alcuni fotogrammi o annunci o contenuti visualizzati. Si tratta di una limitazione della piattaforma e del modo in cui l’inserimento di annunci funziona con TVSDK su iOS.
* La decisione di saltare avviene sull&#39;evento di ricerca in questo caso. Tuttavia, poiché le durate del segmento dell’annuncio nel manifesto non rappresentano con precisione la durata effettiva dell’annuncio, la ricerca non è accurata da un fotogramma. Di conseguenza, puoi vedere alcuni fotogrammi di annuncio quando vengono applicati i criteri di annuncio.
* È possibile che il video a rotazione della licenza non venga riprodotto su iOS 11 e che venga riprodotto correttamente su iOS 9.x e iOS 10.x.
* Nel supporto VPAID 2.0, se la riproduzione è attiva su AirPlay, gli annunci VPAID vengono saltati.
* La `drmNativeInterface.framework` non si collega correttamente quando la destinazione minima è impostata su iOS7 (o versione successiva).
Soluzione: Specifica esplicitamente il `libstdc++.6.dylib` libreria come segue: Vai a **[!UICONTROL Target]** > **[!UICONTROL Build Phases]** > **[!UICONTROL Link Binary With Libraries]** e aggiungere `libstdc++.6.dylib`.
* Post-roll L&#39;annuncio non viene inserito per sostituire l&#39;API.
* La ricerca di un’interruzione pubblicitaria (senza uscire da essa) genera una notifica duplicata di inizio e interruzione annuncio
* Impostazione `currentTimeUpdateInterval` non ha alcun effetto.
Nota: In alcune versioni di iOS, il sistema operativo non carica le risorse all&#39;interno di `PSDKLibrary.framework` automaticamente. È importante copiare manualmente il `PSDKResources.bundle` alle risorse del bundle dell&#39;applicazione: Vai a **Fasi di creazione** e copia le risorse del bundle.
* Non è possibile creare l&#39;app di riferimento utilizzando Xcode 8 o versioni precedenti. A partire dalla versione 1.4.41 di iOS TVSDK, utilizza Xcode 9 per la compilazione.
* Gli annunci VPAID non rispettano il `delayAdLoadingTolerance` valore.
* 24077- Per alcuni contenuti HLS con sottotitoli, il lettore si arresta _Interrompi_ o _Reimposta_ metodo .
* Le notifiche di errore dettagliate non sono disponibili nel caso in cui la risoluzione Just in Time Ad sia abilitata.
* Le notifiche di errore vengono registrate in base al tempo di risoluzione dell&#39;annuncio e non in base alla sequenza dell&#39;annuncio.
* Il supporto HEVC presenta le seguenti limitazioni in questa versione
   * DRM non supportato
   * Supporto CC (CEA 608/708) non disponibile in quanto non supportato in CMAF.
   * Il supporto 4K non è ancora presente.
   * I tag ID3 non sono supportati in quanto non sono supportati in CMAF.
   * Flussi HEVC live non modificati non verificati.
   * Supporto di HEVC Ads non verificato.
* Con JIT abilitato e la tolleranza impostata su 10 secondi, non viene visualizzata alcuna chiamata VAST per la prima interruzione di annuncio multimediale se sono presenti annunci di reindirizzamento VMAP > VAST.
* Affinché il time-out della risoluzione degli annunci funzioni correttamente, ogni volta che la playlist viene aggiornata durante la riproduzione in streaming live, il lettore si aspetta una playlist unita entro 20 secondi. Se non riceve una playlist unita entro tale intervallo, viene generato un errore interno e il lettore si arresta.

## Risorse utili {#helpful-resources}

* [Guida a TVSDK 3.4 per programmatori iOS](/help/programming/tvsdk-3x-ios-prog/ios-3x-introduction/ios-3x-overview/ios-3x-overview.md)
* [Riferimento API per TVSDK iOS 3.4](https://help.adobe.com/en_US/primetime/api/psdk/appledoc_v34/index.html)
* Consulta la documentazione completa dell’Aiuto all’indirizzo [Informazioni e supporto per Adobe Primetime](https://experienceleague.adobe.com/docs/primetime.html) pagina.
