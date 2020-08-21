---
title: Note sulla versione di TVSDK 1.4 per desktop HLS
seo-title: Note sulla versione di TVSDK 1.4 per desktop HLS
description: Le note sulla versione di TVSDK per Desktop HLS descrivono i problemi nuovi o modificati risolti e noti in TVSDK DHLS.
seo-description: Le note sulla versione di TVSDK per Desktop HLS descrivono i problemi nuovi o modificati risolti e noti in TVSDK DHLS.
uuid: 84da27b7-299b-478d-88f5-ef943f0a8321
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: release-notes
discoiquuid: e4437a26-9454-4da1-ae87-0fce664aac3d
translation-type: tm+mt
source-git-commit: 6da7d597503d98875735c54e9a794f8171ad408b
workflow-type: tm+mt
source-wordcount: '5222'
ht-degree: 0%

---


# Note sulla versione di TVSDK 1.4 per desktop HLS {#tvsdk-for-desktop-hls-release-notes}

Le note sulla versione di TVSDK per Desktop HLS descrivono i problemi nuovi o modificati, risolti e noti in TVSDK DHLS.

## Nuove funzioni {#new-features}

**1.4.31**

* **Supporto multi-CDN per annunci CRS**

   * Per impostazione predefinita, tutte le risorse transcodificate saranno ospitate  CDN di proprietà del Adobe su Akamai. Con la versione più recente,  Adobe Creative Repackaging Service (CRS) consente di caricare i creativi transcodificati in più CDN, come specificato dal cliente.
   * Nuove API vengono aggiunte a TVSDK per abilitare la specifica dell&#39;URL creativo CRS finale quando l&#39;URL predefinito non è utilizzato. Per informazioni sull&#39;utilizzo di queste nuove API, consultate la documentazione.

### Nuove funzioni nelle versioni precedenti {#new-features-previous}

**1.4.30**

* **Metriche di fatturazione**

Per ospitare i clienti che desiderano pagare solo per ciò che utilizzano, piuttosto che per un tasso fisso, indipendentemente dall&#39;uso effettivo,  Adobe raccoglie le metriche di utilizzo e utilizza queste metriche per determinare quanto addebitare ai clienti.

**1.4.24**

* **Connessione di rete permanente**

Importante: È necessario avere installato almeno  Flash Player Adobe versione 22 o successiva.
Le connessioni di rete persistenti creano e memorizzano un elenco interno di connessioni di rete che possono essere riutilizzate per più richieste, invece di aprire una nuova connessione per ogni richiesta di rete. Le connessioni di rete persistenti dovrebbero aumentare l&#39;efficienza e diminuire la latenza nel codice di rete.

In questa versione, questa funzione non è supportata in Apple Safari e Mozilla Firefox su Mac.

**1.4.19**

* Supporto dell&#39;integrità del flusso per gli annunci VPAID.
* Abilitata l&#39;opzione di scheda Disattiva audio nel lettore Flash FP 20.0.0.267 per Firefox 42 e versioni successive, risolvendo il problema di blocco.

**1.4.18**

* Primetime Desktop HLS TVSDK ora supporta i creativi SWF lineari VPAID 2.0 per abilitare un&#39;esperienza pubblicitaria interattiva avanzata.

**1.4.10**

* **Ad Fallback, Daisy concatenamento nella logica di selezione degli annunci (Zendesk #3103)** Per annunci VAST (creativi) con la regola di fallback abilitata, TVSDK tratta un annuncio con un tipo MIME non valido come annuncio vuoto e tenta di utilizzare gli annunci di fallback al suo posto. Potete configurare alcuni aspetti del comportamento di fallback.

Per ulteriori informazioni, vedi [Fallback annunci per annunci](../programming/tvsdk-1.4-for-android/ad-insertion/ad-fallback/android-1.4-ad-fallback.md)VAST e VMAP.

**1.4.8**

* **Video Heartbeats Library (VHL) aggiornato alla versione 1.5**

   * Possibilità di inviare i metadati con inizio video e/o inizio video/ad/capitolo come dati contestuali
   * Minore traffico di rete - I battiti di calore sono minori in media e di dimensioni inferiori.

**1.4.7**

* **Supporto per l&#39;individuazione locale**

Supporto per le installazioni locali del  Adobe Individualization Server per personalizzare la richiesta di individualizzazione del client per passare a un endpoint diverso.

**1.4.6**

* **Cifratura AES di esempio (richiede la versione di Flash Player 17.0.0.134)**

È ora supportata la crittografia AES basata su esempio.

**1.4.2**

* **Video Heartbeats Library (VHL) aggiornamento alla versione 1.4.0.1**

   * Aggiunta la possibilità di raggruppare diversi casi di utilizzo di analisi, da altri SDK o lettori, con  Adobe Analytics Video Essentials.
   * Il tracciamento degli annunci è stato ottimizzato rimuovendo i metodi trackAdBreakStart e trackAdBreakComplete. L’interruzione dell’annuncio viene ricavata dalle chiamate dei metodi trackAdStart e trackAdComplete.
   * La proprietà playhead non è più necessaria per il tracciamento degli annunci.

**1.4.0**

* **Segnalazione di blackout con sostituzione** di contenuti alternativi Nel quadro dell’aggiornamento TVSDK 1.4, TVSDK ora supporta anche l’accesso e la restituzione dai blackout regionali rispetto ai contenuti lineari. Il TVSDK ora può elaborare due file manifest in parallelo, principale e alternativo, per monitorare i segnali di blackout anche quando la programmazione alternativa viene mostrata al posto della programmazione originale.

* **Rimuovi/Sostituisci annunci** C3 Ora, non è necessario alcun lavoro di preparazione aggiuntivo per inserire dinamicamente nuovi annunci nelle risorse video-on-demand (VOD) che escono dalla finestra C3. TVSDK fornisce ora un&#39;API per rimuovere intervalli di contenuto personalizzati e inserire nuovi annunci in modo dinamico. Questa nuova potente funzionalità è utile anche nei casi in cui i contenuti live/lineari vengono inviati in onda durante la trasmissione e immediatamente ridotti per essere utilizzati come contenuti on demand senza il tempo necessario per &quot;pulire&quot; la risorsa.

## Problemi risolti {#resolved-issues}

>[!NOTE]
>
>Tutti i clienti TVSDK che utilizzano CRS sono invitati ad effettuare l&#39;aggiornamento ad almeno TVSDK 1.4.32 su iOS, Android e HLS desktop. Questo aggiornamento sostituirà l&#39;implementazione dell&#39;app esistente con un componente aggiuntivo. Dopo l&#39;aggiornamento, verificate che CRS richieda URL creativi in uno strumento proxy (ad esempio, Charles) per verificare che la versione nel percorso rifletta la versione 3.1. Ad esempio,
>
>`https://adunit.cdn.auditude.com/assets/3p/v3.1/218747/94b/c1b/94bc1b964cc67e115a5a6781c7329b90_ee92607938ffff46b083121f044c2746.m3u8`

**Versione 1.4.41**

* Zendesk #33777 - Il codice SWF del token localhost per la build di distribuzione DHLS è scaduto.

   Aggiornamento del token localhost per la demo PMP su DHLS.

### Risolti i problemi nelle versioni precedenti {#resolved-issues-previous}

**Versione 1.4.38** (891)

* Zendesk #30731 - TVSDK non riproduce più annunci VPAID in un AdBreak.

   È stata corretta la riproduzione di più annunci VPAID in un AdBreak.

* Zendesk #29968 - Doppio Billboard.

   Il lettore video può ripetere l&#39;ultimo segmento di un periodo quando si verifica un interruttore ABR. A causa di questo, a volte, ultimo segmento di preroll ripetuto. Questo è stato corretto.

**Versione 1.4.35** (879)

* Zendesk #26058 - Supporto di eventi VPAID nativi

**Versione 1.4.33** (873)

* Zendesk #21701 - Inviate l&#39;URL creativo originale per la richiesta CRS 1401 invece dell&#39;URL normalizzato.

   Il problema per cui gli URL già reimpostati vengono richiesti per la transcodifica è stato risolto, come richiesto dal back-end CRS.
* Zendesk #26197 - La compressione anamorfica non viene riprodotta nella risoluzione di visualizzazione desiderata.

   **Nota**: Questo problema richiede il lettore Flash 24.0.0.194 o successivo.

   È stato risolto il problema per cui le voci mancanti nelle tabelle delle proporzioni venivano utilizzate per calcolare la larghezza di output.

* Zendesk #26840 - Rilevamento HDCP non riuscito su IE11 + Windows7 dopo il secondo tentativo.

   **Nota**: Questo problema richiede il lettore Flash 24.0.0.218 o versione successiva.

   Questo problema è stato risolto modificando l&#39;elaborazione della coda messaggi principale di AdobeCP in modo che si ripetesse attraverso l&#39;intera coda, invece di bloccare solo il primo messaggio.

* Zendesk #27460 - Il nuovo account Akamai non è in grado di gestire una richiesta CDN POST.

   Il nuovo account CDN non è in grado di gestire una richiesta CDN POST. Questo problema è stato risolto aggiornando il codice in modo che cdn.auditude.com e la richiesta siano GET invece che POST.
* Zendesk #27619 - Arresto anomalo del Flash in Windows 10

   **Nota**: Questo problema richiede il lettore Flash 24.0.0.218 o versione successiva.

   Questo problema è stato risolto impedendo un errore come risultato di URL lunghi.

* Zendesk #28218 - L&#39;evento di tracciamento non viene attivato mentre il plackback dal punto di ripresa

   Questo problema è lo stesso di Zendesk #26592. È stato risolto il problema per cui le operazioni di ricerca erano consentite quando il lettore multimediale si trovava nello stato PREPARATO per i flussi VOD.

**Versione 1.4.32** (867)

* Zendesk #26592 L&#39;evento di tracciamento non si attiva quando la riproduzione inizia dal punto di ripresa

Il codice non aggiornava l&#39;elemento di pre-roll annuncio quando il punto di ripresa non era zero. Questo problema è stato risolto aggiungendo logica per aggiornare il codice quando gli orari di inizio dell&#39;intervallo non corrispondono.

* Zendesk #27022 Gli annunci non vengono riprodotti la seconda volta che viene riprodotta una risorsa

Le eccezioni con i metodi array sono state corrette.

**Versione 1.4.30** (855)

In questa versione sono stati risolti i seguenti problemi per TVSDK:

* Zendesk #22898 - I sottotitoli mancanti non dovrebbero causare errori di riproduzione.

**Nota**: Questo problema richiede il lettore Flash 23.0.0.185 o successivo.

Questo problema è stato risolto consentendo a TVSDK di continuare la riproduzione, anche se nel manifesto manca il WebVTT M3U8, e di registrare un avviso.

* Zendesk #23454 - Gli annunci di terze parti (VPAID) non vengono gestiti correttamente

Questo problema è stato risolto gestendo correttamente gli annunci VPAID in base agli ID di contenuto anziché agli intervalli di tempo.

* Zendesk #24528 - Metriche di utilizzo TVSDK per la fatturazione.

Importante: Questo problema richiede il lettore Flash 23.0.0.185 o successivo.

* Zendesk # 25432 Problema dei sottotitoli codificati durante il ridimensionamento del lettore.

Importante: Questo problema richiede il lettore Flash 23.0.0.185 o successivo.

Il codice della mappa texture di visualizzazione della didascalia è stato fissato in modo da gestire correttamente le coordinate durante il ridimensionamento del lettore.

La libreria Video Heartbeat (VHL) è stata aggiornata alla versione 1.5.9 per risolvere i seguenti problemi:

* Zendesk #23730 - Le metriche bitrate sono vuote

Questo problema è stato risolto rilevando le modifiche del bitrate in VideoAnalyticsTracker.

* È stata aggiunta una nuova API, assetDuration, a PTVideoAnalyticsTrackingMetadata per aggiornare la durata delle risorse per i flussi live/lineari.

**Versione 1.4.28** (848)

* Zendesk #25027 - Auditude non funziona nella release desktop 1.4.27

Questo problema è stato risolto aggiungendo il codice per controllare AUDITUDE_METADATA_KEY e intercambiando AUDITUDE_METADATA_KEY e ADVERTISING_METADATA_KEY.

* Zendesk #24428 - Problema frequente di buffering con TVSDK per riprodurre un HLS DRM

Questo problema è stato risolto tenendo conto del fatto che, in assenza di impostazione degli annunci, TVSDK può velocizzare l&#39;elaborazione eliminando il blocco degli annunci pre-roll e la conservazione live sulla timeline progettata per sincronizzare l&#39;inserimento degli annunci.

* Zendesk #24344 - Disabilitare i file WebVTT per migliorare i tempi di avvio.

**Nota**: Questo problema richiede il lettore Flash 23 o successivo.

Questo problema è stato risolto caricando i file WebVTT solo quando è necessario visualizzare le didascalie.

* Zendesk #24994 - I sottotitoli codificati vengono ritirati dal lettore al ritorno da una pausa commerciale

**Nota**: Questo problema richiede il lettore Flash 23 o successivo.

Il codice EOC fittizio causava la scomparsa della visualizzazione della didascalia. Questo problema è stato risolto forzando i codici dei sottotitoli 608 RU2, RU3 e RU4 a fornire la corretta visibilità nella finestra attiva corrente.

**Versione 1.4.27** (844)

* Zendesk #21554 - Segnali di errore TVSDK non attivati per il tipo di applicazione = video/mp4

Questo problema è stato risolto abilitando TVSDK per il ping degli URL di tracciamento errori corretti in formati di risorse non validi.

* Zendesk #23402 - Riproduzione di annunci incompleti

**Nota**: Questo problema richiede il lettore Flash 23 o successivo.

Dopo aver ricevuto un errore 404 su alcune richieste, potrebbe verificarsi un arresto anomalo. Questo problema è stato risolto verificando che la connessione non si chiuda durante la gestione della risposta. La risoluzione assicura che i file VPAID e i file di annunci non vengano conteggiati in modo errato, pertanto non vengono rilasciati durante il download.

* Zendesk #23621 - Il tentativo non riesce su 400 e 404

**Nota**: Questo problema richiede il lettore Flash 23 o successivo.

È stato risolto il problema che causava il danneggiamento dei metadati DRM durante il passaggio tra profili diversi.

* Zendesk #23705 - Blocco degli annunci video durante interruzioni pubblicitarie adStitched

**Nota**: Questo problema richiede il lettore Flash 23 o successivo.

Questo problema è lo stesso di Zendesk #23621.

* Zendesk #23905 - Alcune interruzioni pubblicitarie saltano all&#39;annuncio

**Nota**: Questo problema richiede il lettore Flash 23 o successivo.

Il codice di rete nativo di Windows è stato corretto per garantire che le connessioni non chiudano gli handle attualmente utilizzati da altre connessioni.

* Ticket #24029 - I flussi FER HLS non riproducono tutti gli annunci mid-roll nel file .json mid-roll.

Questo problema è stato risolto consentendo ai client di impostare i parametri personalizzati separatamente sull&#39;istanza Opportunity in modo che i client non debbano ignorare OpportunityGenerator.

**Versione 1.4.26** (839)

* Zendesk #18854 - Aggiornare la logica di selezione creativa in base alle regole CRS
   * È stato fornito il supporto per aggiornare la logica di selezione creativa in base alle regole CRS

* Implementazione di Zendesk #22725 - riproduzioneManager.startPlayback() nell&#39;applicazione di esempio per Desktop

   * È stato risolto il problema rimuovendo questa chiamata ridondante alla fine di startPlaybackFromFlashVars poiché il metodo viene chiamato da setupVideo()

* Zendesk #22807 - Eccezione di riferimento null SeekManager

   * Risolto fornendo la necessaria protezione puntatore NULL all&#39;interno di SeekManager relativa a _dispatcher

* Zendesk #22822 - Buffering frequente quando si utilizza TVSDK per riprodurre un HLS chiaro

   * Risolto rimuovendo l’opportunità iniziale generata da adSignalingModeOpportunityGenerator in assenza di annunci

* Zendesk #23378 - L&#39;integrità del flusso blocca rules.xml

   * È stato corretto caricando il file rules.xml tramite il flusso di lavoro di integrità del flusso di lavoro

**Versione 1.4.24** (817)

* Zendesk #19851 - Quando il lettore si adatta a un bit rate diverso, risale di qualche frame indietro nel tempo al nuovo bit rate, rendendo un&#39;esperienza scomoda

**Nota**: Questo problema richiede il lettore Flash 22.0.0.175 o successivo.

È stato risolto il problema per cui la scheda DRM viene reimpostata dopo il download di una piccola frazione di segmento non viene ripristinata correttamente.

* Zendesk #20784 - Analytics: Attivazione di contenuti completi per transizioni video live

Questo problema è stato risolto aggiungendo un API (trackVideoComplete) per attivare manualmente il completamento del contenuto durante una sessione di tracciamento video LINEAR/LIVE.

Sono state aggiornate le seguenti librerie:

* Zendesk #21643 - Gli annunci VPAID non vengono riprodotti completamente

   * Libreria AdobeMobile alla versione 4.10.0
   * Libreria VHL a 1.5.6
   * Libreria VHL-Nielsen a 1.6.7

Questo problema è stato risolto utilizzando una finestra a altezza zero per riempire l&#39;area di visualizzazione durante la riproduzione di un annuncio VPAID.

* Zendesk #22110 - Analytics: Aggiungere un campo h:sc:ssl alle chiamate di tracciamento heartbeat

I problemi relativi a SSL sono stati risolti e la libreria VHL utilizzata in TVSDK è stata aggiornata alla versione più recente.

* Zendesk #22608 - Video a intermittenza che mostra uno schermo nero (richiede l&#39;Flash Player 22.0.0.175 o successivo)

Durante il bitrate adattivo, con il limite di bitrate massimo, il ricaricamento del video mostra in modo intermittente una schermata nera anche se il client visualizza gli aggiornamenti per la posizione, e il client si comporta come se stesse riproducendo il contenuto.

**Versione 1.4.23** (809)

* Zendesk #2887 - Esito pubblicitario post-roll problema con la logica Regola annunci applicata a TVSDK

**Nota**: Questo problema richiede il lettore Flash 21.0.0.240 o successivo.

È stato corretto il problema per cui gli annunci post-roll venivano ignorati quando la logica della regola degli annunci veniva applicata a TVSDK.

* Zendesk #19863 - Annuncio con file multimediale VPAID scartato

Se un vasto annuncio in linea contiene più file multimediali con un annuncio VPAID che è il primo annuncio, l&#39;annuncio in linea non viene riprodotto per i flussi live. Questo problema è stato risolto raccogliendo un altro file multimediale.

* Zendesk #21021 - Rilegatura ritardata dell&#39;audio con conseguente ripetizione del segmento audio

**Nota**: Questo problema richiede il lettore Flash 21.0.0.240 o successivo.

Il problema di ripetizione audio è stato risolto.

* Zendesk #21125 - Ritorno dall&#39;annuncio live/lineare

**Nota**: Questo problema richiede il lettore Flash 21.0.0.240 o successivo.

Questa versione fornisce supporto per il ritorno da un&#39;interruzione dell&#39;annuncio prima che questa venga riprodotta fino al completamento. La restituzione anticipata è indicata tramite un tag manifest personalizzato.

* Zendesk # 21369 L&#39;audio con associazione tardiva causa di un tempo incoerente

**Nota**: Questo problema richiede il lettore Flash 21.0.0.240 o successivo.

Anche il problema di ripetizione audio risolto è stato risolto.

* Zendesk #21760, 20921 - Audio Video Desync on Seek.

**Nota**: Questo problema richiede il lettore Flash 21.0.0.240 o successivo.

Il problema di ripetizione audio è stato risolto.

* Zendesk #22024 - Errore durante l&#39;esecuzione di TVSDK

È stato risolto il problema per cui il lettore di riferimento che non riproduceva alcun flusso e che generava un&#39;eccezione all&#39;avvio.

**Versione 1.4.22** (791)

* Zendesk #17580 - Errore runtime Primetime con codice 3357

**Nota**: Questo problema richiede il lettore Flash 21.0.0.197 o successivo.

Sono stati corretti gli errori 3357 casuali che si verificavano inizializzando correttamente il deviceID quando viene chiamato storeVoucher().

* Zendesk #21334 - Valore di timeout della richiesta TVSDK per richieste di annunci da parte di terzi

In questa versione, è stato aggiunto il timeout globale per la richiesta di annunci.

**Versione 1.4.21** (782)

* Zendesk #19580 TVSDK attende il completamento del risolutore dei contenuti prima di inviare `PTTimedMetadataChangedNotification` le notifiche

**Nota**: Questo problema richiede il lettore Flash 21.0.0.182 o successivo.

Questo problema è stato risolto in Desktop Reference Player fornendo la possibilità di impostare i tag Ad e aggiungendo un generatore di opportunità personalizzato che mostra come sottoscrivere segnali personalizzati e come elaborare tali segnali in un file VOD.

* Zendesk #20806 Gli annunci mid-roll futuri nella finestra DVR non si attivano dopo la sostituzione delle telecamere

**Nota**: Questo problema richiede il lettore Flash 21.0.0.182 o successivo.

Questo problema è stato risolto aggiornando l&#39;app per impostare _resource.metadata.setValue(DefaultMetadataKeys.ENABLE_LIVE_PREROLL, &quot;false&quot;) per disabilitare l&#39;inserimento di annunci pre-roll in uno scambio PIP e, di conseguenza, non viene generata alcuna opportunità pre-roll.

È stata introdotta una funzionalità di ordinamento per correggere il posizionamento degli annunci fuori sequenza che causava una durata negativa del contenuto principale.

* Zendesk #20522: Impossibile saltare VPAID 2.0 Ads

**Nota**: Questo problema richiede il lettore Flash 21.0.0.182 o successivo.

* Questo problema è stato risolto saltando gli annunci VPAID durante il perdono degli annunci.
* Quando il criterio di interruzione è impostato su Ignora, gli eventi annuncio e annuncio vengono comunque inviati. Lo stato del lettore non è coerente.

Questo problema è stato risolto per comportarsi correttamente e non inviare eventi quando l&#39;interruzione annuncio viene saltata.

* Zendesk #20955 Impostare coppie chiave-valore nella proprietà customParameters tramite il generatore di opportunità

**Nota**: Questo problema richiede il lettore Flash 21.0.0.182 o successivo.

La Richiesta Auditude analizza AuditudeSettings per i parametri personalizzati quando crei un&#39;unità pubblicitaria per le richieste pubblicitarie.

Questo comportamento è stato modificato per includere parametri personalizzati dall&#39;oggetto Opportunità nella richiesta. Inoltre, non è possibile comporre più opportunità con diversi parametri personalizzati in una sola richiesta Auditude.

* Zendesk #21227 - m3u8 non viene riprodotto in modo coerente

**Nota**: Questo problema richiede il lettore Flash 21.0.0.211 o versione successiva.

Questo problema è stato risolto consentendo a TVSDK di ignorare il manifesto (sotto profili HLS) che contiene il codec AC3 non supportato (surround) dal TVSDK.

**Versione 1.4.20** (762)

* Zendesk #19181 - Il gioco dei mattoni va avanti velocemente fino al punto dal vivo si blocca.

**Nota**: Questo problema richiede il lettore Flash 20.0.0.306 o successivo.

* Zendesk #19286 - Flash Player si è verificato un arresto anomalo durante la ricerca avanti e indietro in un flusso FER.

**Nota**: Questo problema richiede il lettore Flash 20.0.0.306 o successivo.

I cambiamenti occasionali che si sono verificati durante la ricerca in Google Chrome sono stati risolti arrestando le query, se le query richiedono troppo tempo per ottenere una risposta o se il socket è stato arrestato.

* Zendesk #19305 - Riproduzione instabile durante la riproduzione di un flusso con discontinuità A/V.

**Nota**: Questo problema richiede il lettore Flash 20.0.0.306 o successivo.

Questo problema è stato risolto segnalando un avviso.

* Zendesk # 19359 - Flash Player arrestato a causa della posizione di #EXT-X-FAXS-CM: nel manifesto a livello di set.

Questo problema è stato risolto quando il tag #EXT-X-FAXS-CM viene visualizzato nella playlist principale prima del bitrate singolo o dei segmenti nella playlist.

* Zendesk #19489 - Fast Forward to Live Point Stalls plugin (flusso live)

Questo problema è lo stesso di Zendesk #19181.

* Zendesk #19699 - TVSDK non passa tra le tracce dei sottotitoli WebVTT

Questo problema è stato risolto creando il dump del lettore e ricaricando il manifesto quando una traccia cambia e correggendo il problema di conversione della stringa UTF8 che ha interessato i nomi di traccia della didascalia WebVTT a doppio byte.

**Versione 1.4.19** (1.4.19.738)

* Zendesk #18234 - Arresti anomali del Flash Player durante la riproduzione dei flussi con stringhe Unicode in CC

Questo problema richiede l&#39;Flash Player FP 20.0.0.267 o successivo ed è stato risolto gestendo correttamente la stringa Unicode.

* Zendesk #18304 - Supporto dell&#39;integrità dei flussi per gli annunci VPAID

Questa funzione richiede l&#39;Flash Player FP 20.0.0.267 o successivo ed è stata introdotta nella release 1.4.19.

* Zendesk #18766 - Il lettore di riferimento non è in grado di visualizzare caratteri unicode non latini nei nomi dei brani CC

Questa funzione richiede l&#39;Flash Player FP 20.0.0.267 o successivo ed è stata risolta gestendo correttamente la stringa Unicode.

* Zendesk #18804 - Arresti anomali del lettore in Firefox 42

Questo problema richiede l&#39;Flash Player FP 20.0.0.235 o successivo ed è lo stesso problema di Zendesk #18723.

* Zendesk #18864 - Flash Player completo arresto del plugin

Questo problema richiede l&#39;Flash Player FP 20.0.0.235 o superiore ed è lo stesso di Zendesk #18723.

* Zendesk #18998 - Se le marche temporali audio e video non corrispondono, si verifica un download infinito dei segmenti in caso di discontinuità.

Questo problema è stato risolto ignorando lo spazio tra marche temporali e semplicemente riproducendo il contenuto scaricato.

* Zendesk #19093 - Gli annunci mid-roll possono essere guardati solo una volta con contenuti live e full-event replay (FER), ma questi annunci non possono essere guardati di nuovo quando si inoltra o si cerca oltre gli annunci

Nel selettore adPolicy predefinito di Primetime, se viene guardato un annuncio mid-roll, adBreak non viene spostato nella posizione cercata al termine della ricerca. Per riprodurre nuovamente l&#39;annuncio, dopo la ricerca, l&#39;applicazione deve sovrascrivere la funzione selectAdBreaksToPlay().

* Zendesk #19101 - Il riavvolgimento in annunci Midroll non risolti rimuove il posizionamento degli annunci.

Questo problema è stato risolto consentendo al lettore di aggiornare l’ora di riproduzioneMetrics, il tempo minimo opportunità e la timeline.

* Zendesk #19102 - Problemi con FER e modalità trucco

Questo problema richiede l&#39;Flash Player FP 20.0.0.267 o successivo ed è stato risolto impostando correttamente la funzione advertisingMetadata.adSignalingMode.

* Zendesk #19175 - A volte gli annunci preroll non vengono visualizzati la prima volta che viene riprodotto il flusso.

Questo problema è stato risolto aggiungendo una nuova API, adRequestTimeout, ad AuditudeSettings per un timeout della richiesta di annunci. Gli utenti ora possono ignorare il timeout predefinito 10 e la richiesta.

**Versione 1.4.18** (1.4.18.722)

* Zendesk #3324 - Il reporting degli annunci Primetime non tiene traccia degli annunci pubblicitari interrotti quando non ci sono annunci multimediali in un VMAP.

Quando un&#39;interruzione pubblicitaria è vuota, gli eventi di tracciamento dell&#39;interruzione dell&#39;annuncio non venivano ping. Questo problema è stato risolto inviando ping di inizio dell&#39;interruzione dell&#39;annuncio su interruzioni pubblicitarie vuote, come VMAP AdBreak, con un nodo AdSource valido.

**Versione 1.4.17** (1.4.17.702)

* Zendesk #17168 - I sottotitoli non vengono visualizzati per 10 secondi dopo aver attivato la visibilità

Questo problema è stato risolto fornendo il supporto per il tag EXT-X-MEDIA-TIME per i file di sottotitoli vtt.

* Zendesk #17983 - Se non si scaricano le chiavi per un manifesto, l&#39;intera riproduzione del manifesto non riesce

**Nota**: È necessario disporre almeno del FP 19.0.0.245 Flash Player o superiore.

In alcuni casi durante la riproduzione di contenuto live, potrebbero essere presenti chiavi non valide nel manifesto (ad esempio, per i periodi di sospensione attività), ma altri intervalli di tempo potrebbero avere chiavi valide e continueranno a essere riprodotti. Precedentemente, quando non era possibile scaricare una chiave elencata in un manifesto, l’intero manifesto non riusciva. Ora, il manifesto non riesce solo quando non è possibile scaricare tutte le chiavi elencate. Se alcune chiavi sono valide, ma non è stato possibile scaricare alcune di queste, il contenuto verrà riprodotto. Se tentiamo di riprodurre un segmento che richiede una chiave non disponibile, continueremo a fallire.

* Zendesk #18554 - Streaming Integrity, che in alcuni casi riduce i cookie

**Nota**: È necessario disporre almeno del FP 19.0.0.245 Flash Player o superiore.

È stato corretto un bug nel codice di manipolazione dei cookie che poteva troncare i valori dei cookie.

**Versione 1.4.16** (1.4.16.684)

* Zendesk #3732 - Aggiungete il supporto per i proxy in Chrome per l&#39;integrità dei flussi (richiede l&#39;Flash Player FP 19.0.0.207 o versione successiva)

Si tratta di un miglioramento.

* Zendesk #4244 - Problemi di streaming al rollover PTS

Questo problema è stato risolto rilevando il rollover e gestendo la discontinuità per tipo di payload e non in modo generico.

* Zendesk #4487 - Tracciamento del canale lineare dei contenuti

Questo problema è stato risolto inizializzando nuovamente il tracciatore heartbeat video durante una sessione di riproduzione del flusso lineare.

* Zendesk #17427 -  Integrità flusso di Adobe non funziona tramite un proxy su Chrome (Win7) ()

**Nota**: La risoluzione richiede il FP Flash Player 19.0.0.2007 o versione successiva.

Questo problema è lo stesso di Zendesk #3732.

* Zendesk #17907 - Ritardo sul flusso live pHLS con Flash Player 19

**Nota**: La risoluzione richiede il FP Flash Player 19.0.0.2007 o versione successiva.

Questo problema è stato risolto gestendo i flussi live in cui i domini dei file TS cambiano quando si ricarica il manifesto live e i file sono stati scaricati due volte.

* Zendesk #17931 - La riproduzione di contenuto HLS con l&#39;ardesia all&#39;inizio non riesce

**Nota**: La risoluzione richiede il FP Flash Player 19.0.0.2007 o versione successiva.

Il problema è stato risolto gestendo i flussi senza audio nei primi 2 secondi del primo file TS.

* Zendesk #17934 - Errore di streaming live con Flash 19.0.0.185

**Nota**: La risoluzione richiede il FP Flash Player 19.0.0.2007 o versione successiva.

Il problema è stato risolto gestendo i flussi live con l&#39;interfoliazione temporale tra i fotogrammi audio e video sui limiti dei segmenti.

* Zendesk #17973 - Ultimo Flash Player 19.0.0.185 arresti anomali durante il mid-roll

**Nota**: La risoluzione richiede il FP Flash Player 19.0.0.2007 o versione successiva.

Il problema è stato risolto gestendo l&#39;audio non muxed con l&#39;inserimento di annunci mid-roll. (Lo switch parser si verifica, e in qualsiasi punto della riproduzione, il contenuto passa all&#39;annuncio mid-roll, o al centro della riproduzione dell&#39;annuncio, e così via.)

* Zendesk #18049 - Flash 19 crash con Firefox 42 beta

Questo problema è lo stesso di Zendesk #17973.

**Versione 1.4.15** (1.4.15.678)

* Zendesk #4377: Incendi evento AD_BREAK_SKIPPED quando salta un&#39;interruzione dell&#39;annuncio a causa del criterio dell&#39;annuncio.

La correzione consisteva nell&#39;aggiungere AD_BREAK_SKIPPED se un annuncio veniva ignorato.

* Zendesk #4496 - Integrità dei flussi: Errore 102100 con reindirizzamenti ai flussi token.

La correzione consisteva nell&#39;aggiungere il supporto per l&#39;impostazione della proprietà AVNetworkConfiguration useCookieHeaderForAllRequests tramite TVSDK.

* Zendesk #17179 - Arresto anomalo del lettore Flash in caso di più modifiche SAP per il contenuto crittografato.

È stato corretto un arresto anomalo durante la riproduzione di alcuni contenuti crittografati.

**Nota**: La correzione richiede l&#39;Flash Player 19.0.0.200 o successivo.

* Zendesk #17499 - come non rimuovere i microlls dopo l&#39;orologio, ma rimuovere preroll dal contenuto del fer

È stato aggiunto un tipo ad AdBreakTimelineItem (AdBreakTimelineItem.placementType) in modo che AdPolicySelector possa restituire un criterio diverso per i contenuti pre-roll, mid-roll e post-roll.

* Zendesk #17665 - Limitazione larghezza di banda

La correzione consisteva nel rimuovere la logica per modificare la dimensione del buffer di destinazione alla dimensione iniziale del buffer all&#39;inizio del buffering.

**Versione 1.14.14** (1.4.14.771)

* Zendesk #17363 - Correggere la documentazione README per il lettore di riferimento

   * Chiarisci le istruzioni per scaricare e installare playerglobal.swc.
   * Aggiungete le istruzioni per l&#39;aggiornamento della configurazione del progetto con una versione specifica del lettore Flash.
   * Aggiornate la configurazione del progetto AdvertisingOverlay per utilizzare la versione minima del lettore.
   * Aggiorna la configurazione del progetto ReferenceCore per utilizzare la versione del lettore specifica 11.9

* Zendesk #17471 - Congelatori

Correzione parziale per un problema per il quale un annuncio non viene riprodotto dall’inizio dopo la ricerca.

* Zendesk #17496 - Podbuster non è stato risolto quando si cercava di nuovo nella finestra DVR

Fornisci parametri personalizzati per ogni interruzione di annuncio.

**Versione 1.4.13** (1.4.13.660)

* Zendesk #4037 - Nessun errore di profilo utilizzabile (richiede l&#39;Flash Player 18.0.0.232 o successivo)

risoluzione del problema di analisi URL quando il parametro di query contiene &quot;http&quot;

* Zendesk #4260 - Flash Player 18 arresti anomali in IE11 (richiede l&#39;Flash Player 18.0.0.232 o successivo)

È stato corretto un arresto anomalo durante la riproduzione di un video in modalità a schermo intero con IE11

* Zendesk #4262 -  arresto anomalo del lettore Adobe Primetime su Windows 10 (richiede l&#39;Flash Player 18.0.0.232 o successivo)

È stato corretto un arresto anomalo durante la riproduzione di un video in modalità a schermo intero con FireFox su Windows.

* Zendesk #4279 - HLS TVSDK inserimento annunci -302 problema di reindirizzamento su iOS e desktop

È stato risolto un problema che impediva all’URL di ottenere il riconoscimento corretto del tipo perché non aveva un’estensione

* Zendesk #4306 - Arresto anomalo del Flash Player quando si attiva lo schermo intero solo su Win (richiede l&#39;Flash Player 18.0.0.232 o successivo)

È stato corretto un arresto anomalo durante la riproduzione di un video in modalità a schermo intero in Windows.

* Zendesk #4480 - Eventi tag ID3 mancanti (richiede Flash Player 18.0.0.232 o superiore)

**1.4.12 **(1.4.12.656)

* Zendesk #2751 - CSAI e CRS | Miglioramento: Gestire gli elementi dinamici in alcuni URL di file multimediali.

Creative Repackaging Service è stato aggiornato per gestire correttamente gli annunci con URL creativi dinamici.

* PTPLAY - 2114 - Supporto per la riproduzione MP4.

È ora supportata la riproduzione di base di contenuti MP4, inclusi riproduzione, pausa e ricerca.

Per quanto riguarda i seguenti requisiti è necessario Flash Player 18.0.0.225 o superiore:

* Zendesk #3992 - Velocità aggiuntive di TrickPlay.

TrickPlay ora accetta frequenze superiori a 16x: +/- 32, +/-64 e +/-128.

* Zendesk #3113 - Flash Player plug-in crash

È stato corretto un arresto anomalo durante il tentativo di riprodurre un annuncio di reindirizzamento su Mac Firefox.

* Zendesk #4037 - Nessun errore di profilo utilizzabile
* Zendesk #4262 -  lettore Adobe Primetime si blocca su Windows 10

È stato corretto l’arresto anomalo di Windows Firefox durante la riproduzione a schermo intero.

**Versione 1.4.11** (1.4.11.648)

* Zendesk #1869 - Modifica delle dimensioni dei font (richiede l&#39;Flash Player 18.0.0.200)

Consentire l&#39;utilizzo delle dimensioni delle didascalie nel codice delle didascalie WebVTT.

* Zendesk #3113 - Flash Player Plugin Crash (richiede l&#39;Flash Player 18.0.0.200)
* Zendesk #3268 - Desktop: Il lettore video inizia lo sfarfallio dopo +- 40/50 secondi e inizia a scattare dopo +- 90 secondi (richiede Flash Player 18.0.0.200)

Correggere il bug relativo al video dell’area di visualizzazione.

* Zendesk #3670 - Errore INVALID_PARAMETER in VOD durante la ricerca nel lettore di riferimento (richiede l&#39;Flash Player 18.0.0.200)

InvalidateProfiles in ThreadSeek quando viene rilevato un nuovo periodo.

* Zendesk #3896 - Arresto anomalo del Flash Player con l&#39;integrità del flusso impostato su ON su Chrome (richiede l&#39;Flash Player 18.0.0.200)

È stato corretto un arresto anomalo in modalità di rete nativa nel pepe

* Zendesk #3905 - Il lettore TVSDK non si carica se ospitato su CDN

Sono stati risolti dei problemi durante la ricerca del token del carattere jolly quando pageDomain è diverso dal dominio swf.

**Versione 1.4.10** (1.4.10.642)

* Zendesk #3249 - Flash di arresto anomalo di TVSDK Web Player su Firefox

È stato corretto un Flash Player occasionale con Firefox su Mac quando un flusso, riprodotto su un monitor esterno, passava a un flusso bitrate più alto.(richiede l&#39;Flash Player 18.0.0.160)

* Zendesk #3268 - Desktop: Il lettore video inizia lo sfarfallio dopo `+-` 40/50 secondi e inizia a scurire dopo `+-` 90 secondi

È stato risolto un problema su Mac Chrome a causa del quale il flusso iniziava a sfarfallare e alla fine diventava nero. (richiede l&#39;Flash Player 18.0.0.161)

* Zendesk #3304 - VAST 3.0 `[ERRORCODE]` macro non popolata

   * il codice di errore 400 sarà esposto se l&#39;annuncio in linea ha un cattivo creativo.
   * `[ERRORCODE]` macro verrà codificata nell&#39;URL

* Zendesk #3601 - Richiesta di miglioramento: Wrapper accompagnatore gestione

   * TVSDK mostrerà la companion di wrapper che contiene le risorse (html, iframe o static) che vengono chiuse in linea. (se l&#39;inline non ne contiene uno per quella dimensione)
   * I wrapper associati a risorse, a meno che non siano utilizzati per la visualizzazione, verranno ignorati. (non utilizzato per il tracciamento)
   * Solo i partner di wrapper con NESSUNA risorsa verranno utilizzati a scopo di tracciamento. (accompagnatore che contiene solo tracciamento)

**Versione 1.4.9**

* Zendesk #2615 - eliminazione della visualizzazione HLS dal display del desktop

È stato aggiunto il metodo clearVideo() a MediaPlayer. Cancella il fotogramma video visualizzato cancellando l&#39;AVStream dall&#39;oggetto StageVideo. Deve essere chiamato solo se il video è in pausa e deve essere chiamato replaceCurrentResource o replaceCurrentItem prima che sia possibile richiamare play().

* Zendesk #3169 - Aggiornamento del lettore di riferimento con  integrazione Adobe Analytics

Il lettore di riferimento è stato aggiornato con &#39;integrazione Adobe Analytics

* Zendesk #3296 - Desktop HLS TVSDK - VAST 3rd Party ads not play

i tipi mime per il formato HLS erano sensibili alla distinzione tra maiuscole e minuscole, non erano corretti e sono stati modificati in modo da non distinguere più la distinzione tra maiuscole e minuscole

**Versione 1.4.8**

* Zendesk #2737 - Desktop Player - Errore 106000 (richiede l&#39;Flash Player 17.0.0.184)
* Zendesk #3007 - Annunci pre-roll non visualizzati dopo l&#39;aggiornamento all&#39;Flash Player 17 (richiede l&#39;Flash Player 17.0.0.184)
* Zendesk #3085 - Il lettore HLS desktop genera 106000 Errore dopo 60 secondi (richiede l&#39;Flash Player 17.0.0.184)

**Versione 1.4.7**

* Zendesk #2760 - Tag DISCONTINUITY ignorato durante la modalità TrickPlay (richiede la versione di Flash Player 17.0.0.158)
* Zendesk #2760 - Tag DISCONTINUITY ignorato durante la modalità TrickPlay (richiede la versione di Flash Player 17.0.0.158)

**Versione 1.4.6**

* Zendesk #2652 - Documentazione Auditude per desktop HLS, Auditude media_id per desktop documentazione HLS

**Versione 1.4.5**

* Zendesk #2256 - Accesso alla sequenza di riproduzione principale, aggiornamento di PSDK per l&#39;invio di eventi TimedMetadata per i tag sottoscritti nella playlist principale. (richiede la versione di Flash Player 17.0.0.134)
* Zendesk #2417 - Lettore che tenta di scaricare i sottotitoli prima dell&#39;avvio della riproduzione, WebVTT utilizzava la variabile del numero di segmento errata per la corrispondenza del numero di segmento. Il bug veniva visualizzato solo per i supporti che avevano indici di segmento a partire da zero. (richiede la versione di Flash Player 17.0.0.134)
* Zendesk #2537 - Arresto anomalo del lettore Flash quando si utilizza il plugin pepe con Chrome (richiede la versione di Flash Player 17.0.0.134)
* Zendesk #2547 - Sottotitoli in arabo: Il testo deve essere allineato a destra (richiede la versione di Flash Player 17.0.0.134)

**Versione 1.4.4**

* Zendesk #1561 - Re: `[Adobe Primetime]` Aggiorna: Supporto del failover basato su client HLS per PROGRAM-DATE-TIME in PSDK desktop (richiede la versione di Flash Player 16.0.0.305 o successiva)
* Zendesk #2197 - `[Ads]` Tracciamento ed errori
* Zendesk #2286 - Richieste di funzioni: Fornire informazioni sullo stato di caricamento degli annunci (VPAID)
* Zendesk #2285 - Richiesta di funzioni: Ignora annuncio dopo una durata di timeout specificata
* Bug #3921755 - Aggiornamento della libreria OpenSSL alla versione 1.0.1L nel Flash Player (richiede la versione di Flash Player 16.0.0.305 o successiva)

**Versione 1.4.2**

* Zendesk #1303 - Offset verticale per i sottotitoli codificati (richiede la versione di Flash Player 16.0.0.235 o successiva, data di rilascio prevista: dicembre 2014)
* Zendesk #1870 - Sottotitoli codificati Accensione e disattivazione (richiede la versione di Flash Player 16.0.0.235 o successiva, data di rilascio prevista: dicembre 2014)
* Zendesk #2110 - La riproduzione si blocca dopo aver provato ad entrare a schermo intero durante un annuncio VPAID (richiede la versione di Flash Player 16.0.0.235 o successiva, data di rilascio prevista: dicembre 2014)
* Zendesk #2199 - Il giocatore non risponde quando `[VPAID]` cerca un annuncio pubblicitario passato
* Zendesk #2358 - Re: `[Analytics]` Dati capitolo errati

**Versione 1.4.1**

* Aggiornata l&#39;API Blackout per essere coerente con l&#39;implementazione di Android e iOS.

**Versione 1.4.0**

* Zendesk #1024 - Funzione per rimuovere gli annunci dal flusso tramite manifesto
* Zendesk #1423 - Errore di riproduzione HLS durante il blocco del Flash Player (senza errori segnalati)
* Zendesk #1674 - ClosedCaption Non visualizzato, corretta visualizzazione della didascalia 708 quando mancano i codici ETX 0x03.

</p>
</details>

## Problemi noti {#known-issues}

* I sottotitoli codificati non funzionano con il contenuto solo audio, perché il sistema dei sottotitoli richiede il funzionamento del video.
Senza video, non esiste una dimensione di visualizzazione e senza una dimensione di visualizzazione non è possibile visualizzare alcuna grafica per le didascalie.
* L&#39;integrità del flusso è leggermente più lenta in Google Chrome a causa delle restrizioni sandbox Chrome.
* In TVSDK 1.4, se disabilitate autoPlay, potrebbe verificarsi un errore DRM quando il lettore rimane inattivo per almeno un minuto. Per risolvere questo problema, quando disabilitate autoPlay ma precaricate le risorse, modificate `ReferenceCore.as` il contenuto di `onPlaybackManagerPrepared`:

```
if (_playbackManager.autoPlay) {
_playbackManager.play();
} else {
_playbackManager.play();
_playbackManager.pause();
}
```

* **Versione 1.4.13** PTPLAY-8501 - Quando VMAP restituisce due annunci diretti MP4 non transcodificati, lo stesso fall back e lo stesso viene riprodotto due volte.

* **Versione 1.4.2** Nella versione di Flash Player 16, un problema è stato identificato con la logica di &quot;switching down&quot; di ABR, dopo che il lettore si è trasformato in un evento di buffering vuoto. Il problema impedisce la disattivazione del bitrate in ambienti con larghezza di banda non corretta quando il lettore entra in uno stato di buffering. Per risolvere il problema, accertatevi che l&#39;app `BufferControlParameters.initialBufferTime` sia impostata come `BufferControlParameters.playbackBufferTime` temporaneamente durante lo stato di buffering (ovvero, su un `BufferEvent.BUFFERING_BEGIN` evento), quindi reimpostatela sui valori impostati per l&#39; `BufferEvent.BUFFERING_END` evento. La correzione di questo problema sarà disponibile nella prossima release della patch dell&#39;Flash Player 16.

* **Versione 1.4.0**

   * PTPLAY-1634 - Lo stesso tag Subscribed ha marche temporali diverse in diverse finestre dal vivo. Quando le finestre attive si spostano, lo stesso tag in ognuna di esse deve avere le stesse marche temporali. Tuttavia, a volte gli stessi tag hanno marche temporali diverse.
   * PTPLAY-28: la timeline di MediaPlayer non include interruzioni vuote.
   * Per l&#39;autorizzazione per lo streaming di contenuto da un dominio diverso è necessario un file di criteri per domini diversi (crossdomain.xml). [Impostazione di un file crossdomain.xml per lo streaming](https://www.adobe.com/devnet/adobe-media-server/articles/cross-domain-xml-for-streaming.html)HTTP.
   * Bug #3694203 - In un flusso DVR, la ricerca dall&#39;interno di un mid-roll di riproduzione in un altro mid-roll ad cue può portare al blocco del browser
   * Bug #3753725 - selectPolicyForSeekIntoAd non prende in considerazione se l&#39;interruzione dell&#39;annuncio è stata osservata
   * Bug #3754529 - Gli annunci pre-roll non vengono rimossi dal flusso quando si cerca di nuovo in un flusso DVR live
   * Bug #3761896 - Se la ricerca è consentita durante la riproduzione di un annuncio, i marcatori di annunci si regoleranno nuovamente dopo la ricerca. La soluzione alternativa non consiste nell&#39;utilizzare il callback ITEM_UPDATED durante la ricerca
   * Bug #3779889 - La chiamata completa non viene effettuata al termine del gioco a 360 gradi in Video Analytics
   * Bug #VA-779 - L&#39;heartbeat dell&#39;evento di cambiamento del bitrate non viene inviato per l&#39;analisi video avanzata con l&#39;implementazione di riferimento del supporto Heartbeat - La riproduzione dei mattoni non è implementata nell&#39;applicazione di esempio.

## Risorse utili {#helpful-resources}

* Consulta la documentazione completa della guida [pagina Informazioni e supporto](https://helpx.adobe.com/support/primetime.html) di Adobe Primetime.
