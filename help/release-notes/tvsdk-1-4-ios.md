---
title: Note sulla versione di TVSDK 1.4 per iOS
seo-title: Note sulla versione di TVSDK 1.4 per iOS
description: Note sulla versione di TVSDK 1.4 per iOS descrivono le novità o le modifiche, i problemi risolti e noti e i problemi del dispositivo in TVSDK iOS 1.4
seo-description: Note sulla versione di TVSDK 1.4 per Android descrivono le novità o le modifiche, i problemi risolti e noti e i problemi del dispositivo in TVSDK iOS 1.4
uuid: c1df12bd-aa21-47e8-ade4-1e497882ce9b
products: SG_PRIMETIME
topic-tags: release-notes
discoiquuid: 452f8699-7857-49ab-9caa-22204b19fe4a
translation-type: tm+mt
source-git-commit: d2b8cb67c54fadb8e0e7d2bdc15e393fdce8550e
workflow-type: tm+mt
source-wordcount: '6578'
ht-degree: 0%

---


# Note sulla versione di TVSDK 1.4 per iOS {#tvsdk-for-ios-release-notes}

Le Note sulla versione di TVSDK 1.4 per iOS descrivono le novità o le modifiche, i problemi risolti e noti e i problemi del dispositivo in TVSDK iOS 1.4.

## Nuove funzioni {#new-features}

**Versione 1.4.45**

* Per conformarsi a Xcode10, TVSDK è stato spostato da &quot;`libstdc++`&quot; a &quot;`libc++`&quot; e di conseguenza la versione minima supportata è iOS 7. Precedentemente era iOS 6.

**Versione 1.4.44**

* Nessuna nuova funzione o miglioramenti in questa versione.

**Versione 1.4.43**

* Esperienza simile a quella televisiva, grazie alla quale è possibile partecipare al mezzo di un annuncio senza attivare il tracciamento parziale degli annunci.\
   Esempio: L&#39;utente si unisce al centro (a 40 secondi) di un annuncio pubblicitario di 90 secondi composto da tre annunci da 30 secondi. Questo è 10 secondi dopo il secondo annuncio nell&#39;interruzione.

   * Il secondo annuncio viene riprodotto per la durata rimanente (20 sec) seguita dal terzo annuncio.
   * I tracciatori di annunci per l&#39;annuncio parziale riprodotto (secondo annuncio) non vengono attivati. Vengono attivati solo i tracciatori del terzo annuncio.

* È stata aggiunta la proprietà enableVodPreroll di tipo booleano nell&#39;interfaccia PTAdMetadata. La proprietà può essere utilizzata per abilitare il pre-roll su un flusso VoD. Se enableVodPreroll è NO, PSDK non viene riprodotto pre-roll. Questo, tuttavia, non ha alcun impatto sui midroli. Il valore predefinito di enableVodPreroll è YES.
* closedCaptionDisplayEnabled API dell’interfaccia PTMediaPlayer è contrassegnata come obsoleta a partire da iOS v1.4.43. Per determinare se sono disponibili sottotitoli codificati per un dato PTMediaPlayerItem, esaminare la proprietà subtitleOptions di PTMediaPlayerMediaItem.

**Versione 1.4.42**

In questa versione non vengono aggiunte nuove funzioni. Per un elenco dei problemi risolti, consultate Problemi risolti.

**Versione 1.4.41**

Modifiche API:

* **isSecure**: È stata introdotta una nuova API isSecure per impedire al lettore di registrare e generare un errore. Il valore predefinito è true.
* **allowExternalRecording**: È stata introdotta una nuova API per consentire il mirroring della riproduzione aerea per un contenuto protetto. Il mirroring di Airplay viene trattato come registrazione, pertanto il valore allowExternalRecording deve essere impostato su &quot;True&quot;, per consentire il mirroring di airplay o impostato su &quot;False&quot; per arrestare il mirroring di airplay per il contenuto protetto. Per impostazione predefinita, il valore è true.

**Versione 1.4.40**

Nessuna nuova funzionalità.

**Versione 1.4.39**

* IOS TVSDK è certificato con VHL 2.0.1 e con VHL 2.0.1 con Nielsen.
* L&#39;SDK per iOS TVSDK viene aggiornato per effettuare richieste CRS dal nuovo host Akamai `primetime-a.akamaihd.net`.
* La nuova configurazione del nome host consente la distribuzione delle risorse CRS sia tramite HTTP che HTTPS (SSL) su scala maggiore.

**Versione 1.4.36**

Integrare e certificare VHL 2.0 in iOS TVSDK: Ridurre la barriera nell&#39;implementazione di VideoHeartbeatsLibrary diminuendo la complessità delle API.

**Versione 1.4.34**

* Informazioni annuncio di rete

   Le API TVSDK ora forniscono informazioni aggiuntive sulle risposte VAST di terze parti. Ad ID, Ad System e VAST Ad Extensions sono forniti in `PTNetworkAdInfo` classe accessibili tramite `networkAdInfo` la proprietà su una Ad Asset. Queste informazioni possono essere utilizzate per l&#39;integrazione con altre piattaforme di Ad Analytics come **Moat Analytics**.

**Versione 1.4.31**

* **Metriche** di fatturazione Per soddisfare i clienti che desiderano pagare solo per ciò che utilizzano, piuttosto che per un tasso fisso indipendentemente dall&#39;uso effettivo,  Adobe raccoglie le metriche di utilizzo e utilizza queste metriche per determinare quanto addebitare ai clienti.

Ogni volta che TVSDK genera un evento di avvio del flusso, il lettore inizia a inviare messaggi HTTP periodicamente a  Adobe  sistema di fatturazione. Il periodo, noto come durata fatturabile, può essere diverso per VOD standard, pro VOD (annunci mid-roll abilitati) e contenuti live. La durata predefinita di ciascun tipo di contenuto è di 30 minuti, ma il contratto con  Adobe determina i valori effettivi.

* **Supporto multi-CDN per** AdsTVSDK CRS ora supporta Multi-CDN per annunci CRS. Fornendo i dettagli FTP per gli annunci CRS, potete specificare posizioni CDN diverse da quelle predefinite  CDN di proprietà del Adobe, ad esempio Akamai.

**Versione 1.4.29**

Nella classe PTSDKConfig, è stata aggiunta l&#39;API forceHTTPS.

La classe PTSDKConfig fornisce metodi per applicare SSL alle richieste effettuate  server Adobe Primetime per le decisioni, DRM e Video Analytics. Per ulteriori informazioni, vedere `forceHTTPS` e `isForcingHTTPS` metodi in questa classe. Se un manifesto viene caricato su HTTPS, TVSDK mantiene l&#39;uso del contenuto HTTPS e lo rispetta quando carica eventuali URL relativi da tale manifesto.

**Nota**: Le richieste ai domini di terze parti come Pixel di tracciamento annunci, URL di contenuti e annunci e richieste simili non vengono modificate, ed è responsabilità dei provider di contenuto e dei server di annunci fornire URL supportati tramite HTTPS.

**Versione 1.4.18**

Primetime iOS TVSDK ora supporta i creativi JavaScript VPAID 2.0 per consentire un&#39;esperienza pubblicitaria interattiva avanzata.

Per ulteriori informazioni su VPAID 2.0, consulta [VPAID e assistenza](../programming/tvsdk-1.4-for-ios/ad-insertion/c-psdk-ios-1.4-vpaid-2.0-ads.md).

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

**Nota**: Il modulo Nielsen è stato rimosso dalla build TVSDK. TVSDK verrà aggiornato prossimamente con un nuovo modulo di integrazione Nielsen.

* **Ad Fallback, catena a margherita nella logica di selezione degli annunci (Zendesk #3103)**

Per gli annunci VAST (creativi) con la regola di fallback abilitata, TVSDK tratta un annuncio con un tipo MIME non valido come un annuncio vuoto e tenta di utilizzare gli annunci di fallback al suo posto. Potete configurare alcuni aspetti del comportamento di fallback.

Per ulteriori informazioni, vedi [Fallback annunci per annunci](../programming/tvsdk-1.4-for-ios/ad-insertion/c-psdk-ios-1.4-ad-fallback.md)VAST e VMAP.

**Versione 1.4.9**

* **Segnalazione Del Blackout Con Sostituzione Alternativa Dei Contenuti**

Come parte dell&#39;aggiornamento 1.4 TVSDK, ora siamo anche in grado di entrare e tornare dai blackout regionali rispetto ai contenuti lineari. Il TVSDK ora può elaborare due file manifest in parallelo, principale e alternativo, per monitorare i segnali di blackout anche quando la programmazione alternativa viene mostrata al posto della programmazione originale.

**Versione 1.4.8**

* **Video Heartbeats Library (VHL) aggiornato alla versione 1.5**

   * Possibilità di inviare i metadati con inizio video e/o inizio video/ad/capitolo come dati contestuali
   * Meno traffico di rete - I battiti cardiaci sono meno in media e di dimensioni più piccole

**Versione 1.4.7**

* **Supporto per l&#39;individuazione locale**

Supporto per le installazioni locali del  Adobe Individualization Server per personalizzare la richiesta di individualizzazione del client per passare a un endpoint diverso.

* **Protezione dell&#39;uscita basata sulla risoluzione**

I criteri DRM ora possono specificare la risoluzione massima consentita, a seconda delle capacità di protezione dell&#39;output del dispositivo. Ad esempio, &quot;Se è disponibile l&#39;HDCP, è possibile riprodurre contenuti con risoluzione fino a 1080p e, se l&#39;HDCP non è disponibile, riprodurre contenuti con risoluzione fino a 480p&quot;.

**Versione 1.4.4**

* **Video Heartbeats Library (VHL) aggiornamento alla versione 1.4.1.1**

   * Aggiunta la possibilità di raggruppare diversi casi di utilizzo di analisi, da altri SDK o lettori, con  Adobe Analytics Video Essentials.
   * Il tracciamento degli annunci è stato ottimizzato rimuovendo i metodi trackAdBreakStart e trackAdBreakComplete. L’interruzione dell’annuncio viene ricavata dalle chiamate dei metodi trackAdStart e trackAdComplete.
   * La proprietà playhead non è più necessaria per il tracciamento degli annunci.
   * È stato aggiunto il supporto per l’ID visitatore Marketing Cloud.

* **Integrazione SDK Nielsen**

   * TVSDK ora supporta l’invio di beacon mTVR e MDPR ID3 all’SDK Nielsen senza alcuna integrazione personalizzata. Per iniziare, scarica l’SDK per app iOS 3.1.2.19 Nielsen.

**Versione 1.4.0**

* **Segnalazione Del Blackout Con Sostituzione Alternativa Dei Contenuti**

   * Come parte dell’aggiornamento 1.4 TVSDK, TVSDK ora supporta anche l’accesso e il ritorno dai blackout regionali rispetto ai contenuti lineari. Il TVSDK ora può elaborare due file manifest in parallelo, principale e alternativo, per monitorare i segnali di blackout anche quando la programmazione alternativa viene mostrata al posto della programmazione originale.

* **Rimuovi/Sostituisci annunci C3**

   * Ora, non è necessario alcun lavoro di preparazione aggiuntivo per inserire dinamicamente nuovi annunci nelle risorse video-on-demand (VOD) che escono dalla finestra C3. TVSDK fornisce ora un&#39;API per rimuovere intervalli di contenuto personalizzati e inserire nuovi annunci in modo dinamico. Questa nuova potente funzionalità è utile anche nei casi in cui i contenuti live/lineari vengono inviati in onda durante la trasmissione e immediatamente ridotti per essere utilizzati come contenuti on demand senza il tempo necessario per &quot;pulire&quot; la risorsa.

## Certificazione e supporto dei dispositivi in 1.4 {#device-certification-and-support-in}

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
* Supporto DRM per imporre HTTPS aggiungendo le API forceHTTPS e isForcingHTTPS.
* Sono state aggiornate le librerie VHL a 1.5.8,  librerie Mobile di Adobe a 4.8.4 e la libreria dell&#39;utilità logger alla versione 7.0 della destinazione di distribuzione.

**Versione 1.4.19**

Questa versione di TVSDK è stata certificata con il supporto FairPlay per iOS e tvOS.

**Versione 1.4.17**

* tvOS

   Questa versione di TVSDK include il supporto per tvOS ed è stata certificata per flussi HLS non crittografati.

   **Nota**: Ricorda le seguenti linee guida per la compilazione:

   * Il supporto TVSDK tvOs è limitato ai flussi crittografati DRM non  Adobe. È necessario rimuovere il riferimento a drmNativeInterface.framework nelle impostazioni di build tvOS. I flussi crittografati AES sono ancora supportati.
   * Apple richiede che tutte le applicazioni Apple TV siano abilitate per il bitcode, pertanto è necessario attivare questo flag nelle impostazioni del progetto.

## Risolti i problemi in 1.4 {#resolved-issues-in}

<!-- 

Comment Type: draft

`<note type="note">` 
 <p>All TVSDK customers who use CRS are strongly encouraged to upgrade to TVSDK 1.4.39 or latest on iOS and Android. This upgrade is a drop-in replacement to the existing app implementation. After the upgrade, check for the CRS creative URL requests in a proxy tool (for example, Charles) to verify that the version in the path reflects version 3.1. For example:</p> 
 <p><span class="code">https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/ 167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784bf3586d.m3u8</span></p> 
`</note>`

 -->

<!-- 

Comment Type: draft

`<note type="note"> `
 <p>TVSDK versions earlier than version 1.4.28 sometimes exhibit a long delay in the startup time when ad-enabled content is played on devices that are running on iOS 10. To resolve this issue, upgrade to version 1.4.28 or later. Version 1.4.28 was released on August 31, 2016, and iOS 10 was released on September 13, 2016.</p> 
`</note>`

 -->

**Versione 1.4.45{#ios-tvsdk}**

* Biglietto #36294 - iOS TVSDK non funzionante con Xcode 10

   * Sono stati corretti i problemi di compilazione con TVSDK su XCode 10. A causa dei requisiti XCode 10, le app create su TVSDK per iOS 1.4.45 in avanti richiedono la destinazione di distribuzione minima come iOS 7.0

* Biglietto #36321 - Discrepanza osservata nell&#39;intervallo ricercabile tra PTMediaPlayer e l&#39;istanza AVPlayer nello stato &quot;Riproduzione&quot;.
* Biglietto #36493 - Supporto `libstdc++` su iOS 12

   * Sono stati corretti i problemi di compilazione con TVSDK su iOS 12. Le app create su TVSDK per iOS 1.4.45 a partire richiedono la destinazione di distribuzione minima come iOS 7.0

**Versione 1.4.44**

* Ticket #34683 - Il Tempo Di Avanzamento Della Riproduzione Degli Annunci Va In Modo Negativo

   * Controlli aggiuntivi per gestire il caso in cui si verificasse una mancata corrispondenza tra la durata indicata dal server degli annunci e il contenuto effettivo degli annunci.

* Ticket #34801 - currentTime e localTime non venivano aggiornati quando si cercava una nuova posizione durante lo stato in pausa

   * L&#39;ora corrente del lettore può ora essere impostata su zero nel caso in cui il lettore sia in stato di pausa; in precedenza, l&#39;ora corrente era impostata su zero solo nello stato di riproduzione.

* Biglietto #35037 - Stalli di riproduzione con URL non corretto al ritorno dall&#39;inserimento di annunci basati su segnali.

   * Correzione migliorata fornita per il problema chiuso #34385 nella release 1.4.42. È stato aggiunto il codice di controllo e gestione delle eccezioni isCanceled per rendere più robusta la coda delle operazioni.

**Versione 1.4.43**

* (ZD#32990) - iOS: Riproduzione dei contenuti invece degli annunci su alcuni cue point. L&#39;API &#39;selectedMediaOptionInMediaSelectionGroup&#39; che faceva parte dell&#39;interfaccia AVPlayerItem ora è stata spostata in AVMediaSelection in iOS 11. Il problema è stato risolto utilizzando questa nuova API.
* (ZD#33683) TVSDK rimosso == suffisso dalle stringhe di metadati. Il problema è stato risolto nella logica di analisi.
* (ZD#33905) - TVSDK iOS per effettuare chiamate ai file manifest con due agenti utente. Il problema relativo all&#39;agente utente è stato risolto nella prima chiamata m3u8 (fresh install case). M3u8 ha gli stessi agenti utente per tutte le chiamate.
* (ZD#34293) - I pre-roll inseriti nei flussi LINEAR non vengono riprodotti correttamente su iOS11. Il problema è stato risolto per gli annunci preroll.
* (ZD#34684) - Quando viene applicato il criterio di salto annunci, le cornici degli annunci pre-roll vengono visualizzate per alcuni secondi. È stata introdotta una nuova API, enableVodPreroll per disabilitare la riproduzione preroll nella riproduzione del video. Il valore predefinito per questa API è &#39;Yes&#39;. L&#39;API assicura che vengano ignorate le cuciture di contenuto degli annunci nel contenuto principale.
* (ZD#34765) - Dopo aver chiamato stop(), alcuni segmenti di flussi di trasporto vengono ancora scaricati. Migliorata l&#39;API Stop() per evitare il download dei segmenti aggiuntivi.
* (ZD#34865) - Gli annunci pre-roll per livestream vengono troncati su iOS. In relazione a iOS11, e aggiungendo un controllo aggiuntivo per confermare se il flusso è pre-roll o contenuto principale, si risolve il problema.
* (ZD#35093) - È stato corretto uno scenario di failover in cui, se la variante principale del flusso non andava a buon fine all&#39;avvio (restituisce 404), la riproduzione non passava al flusso di backup.

**Versione 1.4.42 (1.4.42.118)**

* (ZD#34385) - La riproduzione si blocca con un URL errato quando si torna dall&#39;inserimento di annunci basati su segnali.

   Aumentare i conteggi simultanei massimi per CustomAVAssetLoaderOperations, in modo che le letture del manifesto possano continuare ad essere eseguite.
* (ZD#34373) - Gli utenti finali non possono effettuare lo streaming su dispositivi collegati HDMI, quando la registrazione del flusso non è consentita.
* (ZD#32678) - TVSDK non raccoglie gli ID annunci corretti su iOS.

   L&#39;ID dell&#39;annuncio pubblicitario finale è ora acquisito nei ping VHL in caso di reindirizzamenti VAST/VMAP.
* (ZD#33904) - TVSDK non è registrato per le notifiche AVFFoundation AVAudioSessionMediaServicesAreLostNotification e AVAudioSessionMediaServicesAreResetNotification.

   Ora è possibile registrare nell’app lettore PTMediaServicesIfLostNotification e PTMediaServicesResetNotification per ottenere le notifiche quando i servizi Media vengono reimpostati o persi.

* (ZD#33815) - I clienti non possono aggiornare le proprie regole CRS per la priorità e la normalizzazione senza richiedere un aggiornamento dell&#39;app.

   Sono state aggiunte le API getCRSRulesJsonURL e setCRSRulesJsonURL a iOS TVSDK.

**Versione 1.4.41 (1.4.41.76)**

* (ZD #34464) - Problemi nella creazione dell&#39;app di riferimento con TVSDK versione 1.4.41

   A partire da questa versione, Xcode 9 è richiesto per la compilazione di TVSDK per iOS.
* (ZD #29456) - La partita di volo inizia nello stato sospeso

   È stato corretto il problema di pausa che si verificava quando il video veniva messo in pausa durante l’immissione di una riproduzione aerea.
* (ZD #30371) - L&#39;ora di inizio di AdBreak cambia quando si inseriscono più di 2 annunci nel flusso lineare

   È stato corretto l&#39;errore che si verificava durante il tentativo di riproduzione del contenuto su Apple TV, impedendo la riproduzione completa
* (ZD #32146)- Non viene ricevuto alcun errore PTMediaPlayerStatusError per il contenuto HLS Live sul blocco della versione beta di iOS 11 dev

   Non viene ricevuto alcun PTMediaPlayerStatusError per il contenuto HLS Live e VOD sul blocco tramite Charles (Drop connection e 403)
* (ZD #29242) - La riproduzione video Airplay non riesce con gli annunci attivati

   Quando gli annunci sono attivati e AirPlay è abilitato all’avvio della riproduzione di un video, la riproduzione video non viene mai avviata e non viene visualizzato alcun errore
* (ZD#33341) - DRMInterface.h attiva gli avvisi di creazione in Xcode 9

   Sono stati corretti due prototipi di blocchi in DRMInterface.h per i quali negli elenchi dei parametri mancava la parola &#39;void&#39;
* (ZD#31979) - Non viene compilato/eseguito quando è iOS 10 o versione successiva per iPhone 7/iPhone7+

   È stato corretto il seguente problema: la compilazione di documenti IB per versioni precedenti a iOS 7 non era più supportata
* (ZD#32920) - Schermata vuota entro un&#39;interruzione annuncio e senza completamento interruzione annuncio

   Quando un&#39;interruzione annuncio presenta istanze di annunci e al termine di un&#39;istanza di annuncio, viene visualizzata una schermata vuota
* (ZD#32509) - Disattivazione della registrazione dello schermo iOS 11 Disattivazione della registrazione dello schermo su iOS 11

* (ZD#33179) - Errore di evento intermittente su iOS11

   È stato corretto l&#39;errore di evento su iOS 11

**Versione 1.4.40** (1.4.40.72)

* (ZD #32465) - Il lettore non è in grado di gestire le playlist unite.

   Call FinishLoadingWithError(con: Errore) per la fondazione AV per provare flussi alternativi/attivare il failover.

* (ZD #31951) - Errore TVSDK durante le rotazioni della licenza.

   È stato corretto il problema di rotazione della licenza.
* (ZD #31951) - Schermata vuota entro un&#39;interruzione annuncio e nessun completamento interruzione annuncio.

   È stato risolto un problema per il quale gli annunci VPAID Facebook spesso restituivano più blocchi CDATA in un unico \&amp;lt;AdParameters\&amp;gt; Nodo VAST.
* (ZD #3336) - [iOS] TVSDK - I contenitori degli annunci non vengono compilati, nonostante la quantità di annunci restituiti da FreeWheeler sia sufficiente.

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

* (ZD #29176) - Arresto anomalo su PTAdPolicyDeligate satAdBreakAsWatched:position

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

* (ZD #29462) - TremorHub ad A&amp;E VOD causando un arresto anomalo nelle app iOS

**Versione 1.4.36 (1.4.36.835)**

* (ZD #29418) - I Cues con durata 0 (#EXT-X-CUE-OUT:0.000) causano l’arresto o l’arresto anomalo della riproduzione di iOS TVSDK.

Il problema è stato risolto e la riproduzione viene avviata correttamente.

* (ZD #29462) - Annuncio in VOD che causa un arresto anomalo su iOS TVSDK.

Il problema è stato risolto. L’SDK per iOS TVSDK sta generando un’eccezione (AUDNetworkAdInfo::initWithAdId) e non la gestisce. L&#39;eccezione è dovuta a un ID annuncio vuoto.

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

* (ZD# 28481) - Uscita FER a causa della chiave errata aggiunta alla fine di un&#39;interruzione annuncio per quei flussi FER

Per un flusso FER, il tasto prima dell&#39;interruzione dell&#39;annuncio viene inserito dopo la fine dell&#39;interruzione dell&#39;annuncio. Questo problema è stato risolto aggiungendo l&#39; *ultima chiave* visualizzata alla fine dell&#39;interruzione dell&#39;annuncio.

**Versione 1.4.33** (1.4.33.803 per iOS 6.0+)

* (ZD# 21701) Attivare CRS per i sotto-conti

Abilitata inviando l&#39;URL creativo originale per la richiesta CRS 1401 invece dell&#39;URL normalizzato, come da requisito per il back end CRS.

* (ZD# 26218) - Problema di caricamento PSDKResources.bundle

Questo problema è stato risolto aggiornando il caricamento delle risorse per cercare da tutti i bundle disponibili.

* (ZD# 27460) Prima chiamata Ad Midroll - POST a cdn.auditude<span></span>.com che restituisce 403.

Il nuovo account CDN non è in grado di gestire una richiesta CDN POST. Questo problema è stato risolto aggiornando il codice in modo che la richiesta di `cdn.auditude.com` annuncio fosse GET anziché POST.

**Versione 1.4.32** (1.4.32.792 per iOS 6.0+)

* (ZD# 27132) Supporto per i valori decimali per VMAP Ad Breaks.

Quando il contenuto non era segmentato lungo le interruzioni pubblicitarie definite, i numeri interi causavano inserimenti pubblicitari imprevisti. Il problema è stato risolto non convertendo i valori decimali in numeri interi.

* (ZD# 27189) Il contenuto AES con il tag EXT-X-DISCONTINUITY-SEQUENCE non viene riprodotto correttamente.

Il problema è stato risolto inserendo il tag all&#39;inizio della playlist.

**Versione 1.4.31** (1.4.31.785 per iOS 6.0+)

* (ZD# 24528) Implementare le metriche di utilizzo TVSDK per la fatturazione

Per ulteriori informazioni, vedi Metriche [](../programming/tvsdk-1.4-for-ios/c-psdk-ios-1.4-billing/c-psdk-ios-1.4-billing.md)di fatturazione.

* (ZD# 24642) Supporto Picture-in-Picture per TVSDK

La funzione picture-in-picture, che in alcuni casi non funzionava correttamente, è stata corretta.

* (ZD# 25246) Segnali di interruzione annuncio non corretti

Questo problema è stato risolto allineando i tag di discontinuità tra i vari manifesti.

* (ZD# 26218) Il processo di creazione dell&#39;applicazione si complica quando si tenta di includere PSDKLibrary.framework nel framework dell&#39;applicazione del cliente

Questo problema è stato risolto creando il pacchetto PSDKLibrary.framework come richiesto.

* (ZD# 26364) Supporto multi-CDN per annunci CRS

<!-- 
Comment Type: draft
For more information, see [Multiple CDN support for CRS Ad Delivery](http://help.adobe.com/en_US/primetime/psdk/ios/1.4/index.html#PSDKs-concept-Multiple_CDN_support_for_CRS_ad_delivery).
-->
* (ZD# 27028) Ritardo nella riproduzione di alcuni flussi in iOS 10.

Questo problema è stato risolto fornendo una soluzione alternativa per i flussi che non hanno un&#39;estensione M3U8.

**Versione 1.4.30** (1.4.30.754 per iOS 6.0+)

In questa versione sono stati risolti i seguenti problemi per TVSDK:

* (ZD# 24180) Aggiungere un&#39;intestazione personalizzata al elenco consentiti 

Al elenco consentiti  TVSDK è stata aggiunta una nuova intestazione personalizzata.

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

Questo problema è stato risolto aggiungendo l’API assetDuration per aggiornare la durata delle risorse per i flussi Live/Linear e fornire una logica per il controllo del flusso live. `PTVideoAnalyticsTrackingMetadata`

* (ZD# 22675) VHL - Analytics: Aggiornamento della durata della risorsa video in diretta

Questo problema è lo stesso di ZD #22351.

* (ZD #25908) VHL - Analytics: Arresto anomalo dell&#39;evento Heartbeat  Adobe

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

   * Risolto aggiornando le librerie con il supporto del modulo

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

È stato corretto il problema per cui TVSDK restituiva un errore 101000 durante l&#39;avvio della riproduzione  flussi DRM di accesso Adobe.

* (ZD #21889) - La riproduzione di annunci online e contenuti offline non riesce

È stato corretto il seguente problema: la riproduzione non riusciva dopo che un annuncio pubblicitario su contenuto offline crittografato con AES.

* (ZD #22074) - L&#39;arresto anomalo dell&#39;AUDVAST si verifica una volta al minuto su iOS

Questo problema è stato risolto migliorando la gestione dei tag di annunci VAST di terze parti con caratteri non validi nell&#39;URL.

* (ZD #22257) - Il TVSDK non riproduce il flusso DRM

È stato corretto il problema per cui il TVSDK che restituiva un errore 101000 durante l&#39;avvio della riproduzione  flussi DRM di accesso Adobe.

**Versione 1.4.22** (1.4.22.627) per iOS 6.0+

* (ZD #18709) - Arresto anomalo di TVSDK per iOS

È stato risolto il problema relativo a un arresto anomalo che si verificava in alcuni flussi protetti da DRM di Access  Adobe.

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

**1.4.21** (1.4.21.605) per iOS 6.0+

* (ZD #20749) - Fallback salta le risposte VAST non vuote; Altri URL di tracciamento annunci attivati

È stato risolto un problema relativo ai ping duplicati negli annunci di fallback.

**1.4.20** (1.4.20.590) per iOS 6.0+

* (ZD #18639) - Il TVSDK utilizza CPU/risorse eccessive su una lunga risorsa per la registrazione a caldo

L&#39;utilizzo eccessivo di CPU/risorse è stato corretto nei due livelli. In primo luogo, consentendo l&#39;esecuzione della funzione di aggiornamento del tempo su una coda globale, invece del thread principale, e ottimizzando l&#39;utilizzo della CPU per l&#39;analisi del manifesto con il m3u8 precedentemente elaborato e memorizzato nella cache.

* (ZD #19349) - Gli annunci pre-roll vengono ignorati durante la limitazione della connessione di rete.

Questo problema è stato risolto fornendo un evento di timeout (requestTimeout) all’applicazione e agli adMetadata.  l&#39;API adRequestTimeout per ignorare il timeout predefinito di 10 secondi.

* (ZD #19446) - Notifica mancante nei flussi in diretta

Questo problema è stato risolto consentendo la sottoscrizione dell’applicazione al programma EXT-X-PROGRAM-DATE-TIME sui flussi live.

* (ZD #19459) - Arresto anomalo durante la preparazione di audio alternativo con PTMediaPlayerItem PrepareAudioOptionsWithAVMediaSelectionOptions
* (ZD #19460) - Arresto anomalo - [PTMediaPlayerItem PrepareSottotitoliOptionsWithAVMediaSelectionOptions:nonForcedOptions:]

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

Questo problema è stato risolto consentendo alle applicazioni di impostare il proprio valore di playhead.

* Zendesk #18518 - Se il nome del video non è specificato, per impostazione predefinita il nome di TVSDK è un lettore basato su *PSDK.*

Questo problema è stato risolto rimuovendo il valore predefinito per il nome del lettore.

**Versione 1.4.17** (1.4.17.545) per iOS 6.0+

* Zendesk #2228 - Migliorate il TVSDK per restituire la risposta JSON del recupero di un manifesto

Invece di inviare un errore quando il contenuto non è M3U8, DRM Framework restituisce un DRMMetadata nil. Il problema è stato risolto aggiungendo metadati per esporre il contenuto quando si verifica la notifica M3U8_PARSER_ERROR.

* Zendesk #2231 - Errore restituito dal recupero del manifesto non disponibile in MediaPlayerNotification

Stessa risoluzione di Zendesk #2228

* Zendesk #3304 - VAST 3.0 `[ERRORCODE]` macro non popolata

Problema per il quale l’SDK di Auditude non riesce a inviare un ping quando l’URL di tracciamento ha degli spazi all’inizio è stato risolto.

* Zendesk #17294 - Crash SecKeyRawSign

È possibile che si verifichi un arresto anomalo quando il codice del cliente utilizza la catena di chiavi.

* Zendesk #18008 - Cookie di supporto per iOS8+ per il supporto dei flussi token

I flussi token Akamai richiedono che i cookie vengano inviati sulle richieste dei segmenti, e questo non era possibile su iOS 7 e versioni precedenti. A partire da iOS 8, Apple ha aggiunto un&#39;API che consente il passaggio di cookie per le richieste di segmenti. Questo supporto è ora disponibile in TVSDK. È stato inoltre aggiunto il supporto per l’invio di un agente utente, se disponibile.

* Zendesk #18166 - TVSDK 1.4.15 invia centinaia di avvisi durante la compilazione con DWARF con opzioni di file dSYM

Tutti gli avvisi sono stati risolti.

**Nota**: per TVSDK sono state aggiunte librerie compatibili con tvOS.

**Versione 1.4.16** (1.4.16.1454)

* Zendesk #3875 - Tabulazione S Arresti anomali durante la riproduzione

Ripristino della dipendenza di OKHTTP dall’auditude per CRS in quanto TVSDK ora utilizza direttamente la connessione httpurlconnection invece di curl. Il problema è stato risolto eliminando le eccezioni prima di effettuare un&#39;altra chiamata JNI.

* Zendesk #4487 - Tracciamento del canale lineare dei contenuti

Il problema è stato risolto inizializzando nuovamente il tracciatore heartbeat video durante una sessione di riproduzione del flusso lineare.

* Zendesk #17919 - Android - la ricerca del contenuto causa un errore heartbeat

Il problema era quello di risolvere il heartbeat in stato di errore in caso di ricerca in un capitolo

* Zendesk #18053 - L&#39;applicazione che utilizza l&#39;SDK TVSDK si blocca su Marshmallow

Il TVSDK si arrestava in modo anomalo su Android M OS quando la libreria TVSDK utilizza il codice neon che esegue la conversione colore YUV -> RGB. Questo problema è stato risolto aggiornando le funzioni che causano il problema utilizzando una versione non neon del codice.

* Zendesk #18072 - Android M - Arresto anomalo dell&#39;applicazione

Questo arresto anomalo si verifica quando si chiamano le API MediaCodecList e MediaCodecInfo quando si verifica se il profilo e il livello sono supportati.  Adobe sta cercando il supporto di Google per ulteriori approfondimenti. Questo problema è stato risolto fornendo una soluzione temporanea caricando tutte le informazioni del codec in anticipo per evitare di chiamare queste API solo quando sono necessarie informazioni sul codec.

* Zendesk #18074 - Sottotitoli arabi non funzionanti su Nexus con Android 6.0

Questo problema è stato risolto fornendo il supporto per la mappa dei font CTS per Android.

**Versione 1.4.15** (1.4.15.512) per iOS 6.0+

**Nota**: Il modulo Nielsen è stato rimosso dalla build TVSDK, ma il TVSDK verrà aggiornato prossimamente con un nuovo modulo di integrazione Nielsen.

* (ZD #2228) - Errore restituito dal recupero del manifesto non disponibile in MediaPlayerNotification

Sono stati aggiunti metadati per esporre il contenuto quando si verifica la notifica M3U8_PARSER_ERROR.

* (ZD #4437) - Arresti anomali all&#39;interno  SDK Adobe Primetime

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

* (ZD #2751) CSAI e CRS | Miglioramento: Gestire gli elementi dinamici in alcuni URL di file multimediali.

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

Supporto per il ping di URL vuoti di tracciamento delle interruzioni di annunci, TVSDK verificherà ora l&#39;avvio dell&#39;interruzione di annunci e completerà i ping per interruzioni di annunci vuoti

**Versione 1.4.8** (1.4.8.402)

* (ZD #3158) Arresto anomalo di IOS 7 in Riproduzioni evento complete

**Versione 1.4.7** (1.4.7.382)

* (ZD #2197) Tracciamento degli errori degli annunci. Aggiunta notifica per la risorsa non riuscita a caricare il manifesto.
* (ZD #2894) Player Esegue 4 richieste di manifesto di livello principale durante la riproduzione.
* (ZD #2992) Auditude Segnalare durate e identificatori bizzarri.

**Versione 1.4.6**(1.4.6.325)

* (ZD #2197) Tracciamento degli errori degli annunci. Aggiunta notifica per il caricamento del manifesto della risorsa non riuscita

**Versione 1.4.5** (1.4.5.283)

* (ZD #2141) Implementazione di Analytics per l&#39;app TreeHouse, aggiunta della libreria AdobeAnalyticsPlugin.a per creare il pacchetto.
* Video Heartbeats Library update to 1.4.1.2
* (PTPALY-4226) (relativo a ZD #2423) L&#39;esecuzione di ripristino DRM può comportare l&#39;eliminazione dei dati del documento dell&#39;applicazione.

**Versione 1.4.4** (1.4.4.242)

* Video Heartbeats Library (VHL) aggiornato alla versione 1.4.1.

* (ZD #2435) Documentazione TV SDK sui requisiti di analisi

**Versione 1.4.2** (1.4.2.210: iOS 6.0+)

* (ZD #1129) _player.currentItem.audioOptions che restituisce empty
* (ZD #2109) Primetime PSDK 1.4.1.125 non funziona con Xcode 5.1.1
* (ZD #2137) Arresto anomalo in PSDK su iOS quando non è possibile caricare i metadati DRM

**Versione 1.4.1** (1.4.1.125)

* (ZD #1107) Simboli duplicati del lumberjack
* (ZD #1644) Modificare l&#39;agente utente iOS per il targeting e il reporting
* (ZD #1850) File Lumberjack del cacao inclusi nell’SDK iOS
* (ZD#1908) I tag personalizzati vengono ignorati da PSDK se sono presenti più di 1

**Versione 1.4.0** (1.4.0.32)

* Zendesk #1024 - Funzione per rimuovere gli annunci dal flusso tramite manifesto

## Problemi noti nella versione 1.4 {#known-issues-in}

* In iOS TVSDK, tutti gli annunci vengono inseriti nel manifesto del contenuto. I comportamenti degli annunci vengono implementati ricercando in base alla durata del contenuto e dei segmenti degli annunci. Pertanto, se le durate del segmento non sono precise, la ricerca potrebbe non terminare sempre al fotogramma esatto dell&#39;inizio o della fine dell&#39;interruzione dell&#39;annuncio. Anche se le durate sono al frame, c&#39;è una tolleranza che la piattaforma stessa impone alla ricerca e ci possono essere alcuni fotogrammi o annunci o contenuto visualizzati. Si tratta di una limitazione della piattaforma e del modo in cui l’inserimento di annunci funziona con TVSDK su iOS.
* La decisione di saltare avviene sull&#39;evento di ricerca in questo caso. Tuttavia, poiché le durate del segmento di annuncio nel manifesto non rappresentano con precisione la durata effettiva dell&#39;annuncio, la ricerca non è accurata per i fotogrammi. Di conseguenza, alcuni fotogrammi dell&#39;annuncio vengono visualizzati quando vengono applicati i criteri degli annunci.
* RECORDING_ERROR: Errore durante la registrazione dello schermo.
* È possibile che il video a rotazione licenza non venga riprodotto su iOS 11 e che venga riprodotto correttamente su iOS 9.x e iOS 10.x.
* Nel supporto VPAID 2.0, se la riproduzione è attiva su AirPlay, gli annunci VPAID vengono ignorati.
* drmNativeInterface.framework non si collega correttamente quando la destinazione minima è impostata su iOS7 (o versione successiva).\
   Soluzione: Specificate esplicitamente il `libstdc++6`.  libreria dylib come segue: Vai a Target->Fasi build->Collega binario a librerie e aggiungi `libstdc++.6.dylib`.

* Post-Roll Ad non viene inserito per la sostituzione dell&#39;API.
* La ricerca di un&#39;interruzione di annuncio (senza uscire da essa) rilascia un duplicato e avvia una notifica di interruzione annuncio
* L&#39;impostazione currentTimeUpdateInterval non ha alcun effetto.\
   Nota: In alcune versioni iOS, il sistema operativo non carica automaticamente le risorse all&#39;interno di PSDKLibrary.framework. È importante copiare manualmente il file PSDKResources.bundle nelle risorse del bundle dell’applicazione: Andate a &quot;Fasi build&quot; e copiate le risorse del bundle.
* L&#39;app di riferimento non può essere creata utilizzando Xcode 8 o versioni precedenti. A partire da iOS TVSDK versione 1.4.41, utilizzate Xcode 9 per la compilazione.

## Risorse utili {#helpful-resources}

* Consulta la documentazione completa della guida [pagina Informazioni e supporto](https://helpx.adobe.com/support/primetime.html) di Adobe Primetime.