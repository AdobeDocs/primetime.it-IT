---
title: Note sulla versione di TVSDK 2.4.1 per Android
seo-title: Note sulla versione di TVSDK 2.4.1 per Android
description: Le note sulla versione di TVSDK 2.4.1 per Android descrivono le funzioni nuove e supportate e i problemi e le limitazioni noti in TVSDK Android 2.4.1.
seo-description: Le note sulla versione di TVSDK 2.4.1 per Android descrivono le funzioni nuove e supportate e i problemi e le limitazioni noti in TVSDK Android 2.4.1.
uuid: 929fc577-e851-4e03-9201-13280cc6137a
topic-tags: release-notes
products: SG_PRIMETIME
discoiquuid: a6dbcc4a-9e14-4452-9004-b39ed13fad6f
translation-type: tm+mt
source-git-commit: e644e8497e118e2d03e72bef727c4ce1455d68d6

---


# Note sulla versione di TVSDK 2.4.1 per Android {#tvsdk-for-android-release-notes}

Le note sulla versione di TVSDK 2.4.1 per Android descrivono le funzioni nuove e supportate e i problemi e le limitazioni noti in TVSDK Android 2.4.1.

## TVSDK Android 2.4.1 {#tvsdk-android}

Adobe sta rilasciando TVSDK 2.4.1 per Android.

Per utilizzare questa versione di TVSDK, accertati che il sistema soddisfi i requisiti descritti in Requisiti [di](https://helpx.adobe.com/content/dam/help/en/primetime/programming-guides/psdk_android_2.5.pdf#page=6)sistema.

Qui potete trovare la documentazione:

・ Guida in linea TVSDK 2.4 per Android - Guida

・ [Javadocs TVSDK 2.4 per API Java Android](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/index.html)

I Javadocs sono l&#39;autorità suprema, perché vengono generati automaticamente direttamente dal codice sorgente TVSDK.

・ Documentazione API [C++ TVSDK 2.4 per API Android C++](https://help.adobe.com/en_US/primetime/api/psdk/cpp_2.4/namespaces.html)

Ogni classe Java ha una classe C++ corrispondente, e la documentazione C++ contiene più materiale esplicativo rispetto a Javadocs, pertanto consulta la documentazione C++ per una maggiore comprensione dell&#39;API Java.

・ Guida alla migrazione ([TVSDK 2.4 per Android Migration Guide](../migration-guides/tvsdk-14-25-android.md))

Questa guida spiega cosa devi modificare per migrare un’applicazione basata su TVSDK 1.4 a una basata su TVSDK 2.4.

## Nuove funzioni {#new-features}

TVSDK 2.4.1 per Android offre molti miglioramenti in termini di prestazioni rispetto alle versioni precedenti. Offre un’esperienza visiva di alta qualità.

Questa versione include tutte le funzioni delle versioni 2.4 e 2.4.1 e nessuna funzione è obsoleta.

Di seguito sono riportate le nuove funzionalità principali della versione 2.4.1:

* Funzioni HLS versione 4

   * **Riproduzione** video (riproduzione, pausa, ricerca) con controllo del lettore per flussi live, lineari e VOD.
   * **Sottotitoli codificati.** TVSDK può visualizzare sottotitoli codificati 608/708 con una selezione di font, dimensioni dei font, colori e sfondo. È inoltre possibile supportare i video con didascalie di rollup e passare tra le tracce delle lingue, se disponibili.
   * **La modalità** di riproduzione dei mattoni supporta l&#39;avanzamento rapido e il riavvolgimento per i flussi HLS che utilizzano i frame I. Tutti i controlli di riproduzione video funzionano sul contenuto. Slow motion (in avanti) è disponibile per la modalità di riproduzione video esterna con valori compresi tra 0 e 1.
   * **ABR (Adaptive Bitrate)** consente al lettore di selezionare dinamicamente quale delle versioni multiple dello stesso flusso di contenuti riprodurre, in base alla rete e ad altre condizioni. È possibile impostare i parametri in modo dinamico o nel file manifesto per selezionarli tra criteri di selezione aggressivi, moderati e conservativi.
   * **Gli intervalli** di byte consentono a un singolo file TS di contenere più segmenti TS.
   * **Le rappresentazioni** audio alternative consentono al lettore di passare dalle tracce audio disponibili.
   * **Supporto per ID3.** TVSDK può riprodurre flussi audio e video HLS che contengono metadati audio ID3, come il nome dell&#39;artista, il titolo e l&#39;album.
   * **Failover. **TVSDK utilizza strategie per continuare la riproduzione ininterrotta, nonostante gli errori dei server host, dei file playlist e dei segmenti.
   * **Passaggio audio multicanale (DD+).** TVSDK può trasmettere i dati audio Dolby Digital Plus (E-AC3) all&#39;hardware di supporto.

* Funzioni di protezione dei contenuti

   * **DRM per HLS.** Tutte le API di riproduzione video funzionano con contenuto video crittografato protetto da Adobe Access. Sono supportate le seguenti funzionalità DRM:

      * Rotazione licenza
      * Rotazione chiave
      * Memorizzazione delle licenze nella cache
      * Ora politica
      * IV rotazione

* **Riproduzione AES 128.** TVSDK può riprodurre contenuto HLS avanzato standard (AES) con una dimensione chiave di 128 bit.
* **L&#39;HLS protetto (PHLS)** fornisce un set limitato di criteri DRM pregenerati, un sottoinsieme di ciò che Adobe Access fornisce, per consentire DRM su HLS leggere per i flussi live e VOD.

* Pubblicità/contenuti alternativi e funzioni di monetizzazione

   * **Tracciamento degli annunci inseriti sul lato server.** TVSDK può tenere traccia degli annunci inseriti dal servizio di inserimento annunci di Adobe Cloud. Supporta gli annunci lineari nei formati VAST2, VAST3 e VMAP per i flussi VOD e live/lineari.
   * **Tag HLS personalizzati.** TVSDK utilizza la propria `MediaPlayerConfig` classe per abilitare la notifica all&#39;applicazione del lettore quando i tag HLS personalizzati compaiono nel flusso.
   * **Inserimento annunci lato client.** La libreria Auditude e di inserimento funziona con i server Adobe Auditude per risolvere gli annunci da inserire dinamicamente in contenuti live, lineari e VOD, nelle posizioni pre-roll, mid-roll o post-roll.
   * **Risolutori annunci personalizzati.** Le interfacce `ContentResolver, OpportunityGenerator,` e `MediaPlayerClientFactory` le interfacce consentono di implementare un risolutore di contenuti ad/alternativo personalizzato e di registrare un rilevatore di opportunità personalizzato per lavorare con TVSDK. Le classi `TestAdResolver` e `AuditudeResolver` forniscono esempi C++ di implementazione di un risolutore dei contenuti. Potete trovare un esempio JavaScript in `samples/jspsdk/testapp/psdk.js`.
   * **Comportamento pubblicitario coerente.** Utilizzare l&#39; `AdPolicySelector` interfaccia per abilitare un comportamento coerente tra tutti i lettori per operazioni quali ricerca e trucco quando gli annunci sono presenti nel contenuto. Se non implementate il vostro pacchetto, TVSDK utilizza `DefaultAdPolicySelector`.
   * **Rimuovere/sostituire annunci C3.** Utilizzate l&#39;API TVSDK appropriata per rimuovere intervalli di contenuto personalizzati e inserire dinamicamente nuovi annunci senza ulteriori operazioni di preparazione. Questa funzione è utile per la trasmissione di contenuti live/lineari, per poi renderli immediatamente disponibili su richiesta senza pulizia.

Di seguito sono riportate le nuove funzionalità principali della versione 2.4:

* **Attivato istantaneo per VOD e live** Quando si attiva l’istante, il TVSDK inizializza e crea un buffer per i contenuti multimediali prima dell’avvio della riproduzione. Poiché potete avviare più `MediaPlayerItemLoader` istanze contemporaneamente in background, potete creare un buffer per più flussi. Quando un utente cambia il canale e il flusso si trova correttamente nel buffer, la riproduzione sul nuovo canale inizia immediatamente. TVSDK 2.4 supporta anche Instant On per i flussi live. I flussi live vengono inseriti nuovamente nel buffer quando la finestra live si sposta.

* **Miglioramenti delle prestazioni **La nuova architettura TVSDK 2.4 offre diversi miglioramenti delle prestazioni:

   * **Sottosegmentazione** : TVSDK riduce ulteriormente le dimensioni di ciascun frammento per avviare la riproduzione il prima possibile.
   * **Download** di annunci paralleli - TVSDK prerileva gli annunci in parallelo alla riproduzione del contenuto prima di colpire le interruzioni pubblicitarie, consentendo così la riproduzione senza soluzione di continuità di annunci e contenuti.
   * **Risoluzione** pubblicitaria pigra - Con questa funzione, non aspettiamo la risoluzione degli annunci non preroll prima di avviare la riproduzione, riducendo così il tempo di avvio. Le API come ricerca e trucco non sono ancora consentite fino alla risoluzione di tutti gli annunci.

* **Riproduzione di contenuti MP4**

Questa versione di TVSDK supporta la riproduzione di MP4 come contenuto principale.

* **Connessioni di rete persistenti**

TVSDK gestisce un set di connessioni di rete riutilizzabili, pertanto non comporta il sovraccarico necessario per creare e distruggere una connessione di rete per ogni richiesta di rete.

* **Protezione dell&#39;uscita basata sulla risoluzione**

Questa funzione associa le restrizioni di riproduzione a risoluzioni specifiche, fornendo controlli DRM più precisi.

* **Riproduzione dei mattoni con bitrate adattivo (ABR)**

Questa funzione consente a TVSDK di passare da un flusso di iFrame all’altro in modalità di riproduzione trucco. Potete utilizzare profili non iFrame per eseguire la riproduzione a velocità più basse.

* **Smooth trucco**

Questi miglioramenti migliorano l&#39;esperienza utente:

・ Selezione del bit rate e del frame rate adattivi durante la riproduzione, in base alla larghezza di banda e al profilo del buffer

・ Utilizzare il flusso principale invece del flusso IDR per ottenere una riproduzione rapida fino a 30 fps.

* **Logica ABR migliorata**

La nuova logica ABR si basa sulla lunghezza del buffer, sulla velocità di modifica della lunghezza del buffer e sulla larghezza di banda misurata. In questo modo, l&#39;ABR sceglie il bit rate corretto quando la larghezza di banda oscilla e ottimizza anche il numero di volte in cui l&#39;interruttore del bitrate avviene effettivamente monitorando la velocità con cui cambia la lunghezza del buffer.

* **Fatturazione**

TVSDK raccoglie automaticamente le metriche, rispettando il contratto di vendita del cliente per generare rapporti di utilizzo periodici richiesti a scopo di fatturazione. A ogni evento di inizio flusso, TVSDK utilizza l&#39;API di inserimento dati di Adobe Analytics per inviare metriche di fatturazione quali il tipo di contenuto, i flag abilitati per l&#39;inserimento di annunci e i flag abilitati per l&#39;abilitazione di drm, in base alla durata del flusso fatturabile, alla suite di rapporti di proprietà di Adobe Analytics Primetime. Ciò non interferisce con le suite di rapporti Adobe Analytics o le chiamate server del cliente, né viene incluso in esse. Su richiesta, questo rapporto sull&#39;utilizzo della fatturazione viene inviato periodicamente ai clienti. Questa è la prima fase della funzione di fatturazione che supporta solo la fatturazione dell&#39;utilizzo. Può essere configurato in base al contratto di vendita utilizzando le API descritte nella documentazione.

## Funzioni supportate {#supported-features}

TVSDK per Android 2.4 supporta una serie di funzionalità che potete implementare per aggiungere funzionalità alle applicazioni video.

>[!NOTE]
>
>Nelle tabelle di matrici di feature riportate di seguito, a Ö indica che la feature è supportata nella release corrente.

### Funzioni di riproduzione principali {#core-playback-features}

| **Feature** | **Tipo di contenuto** | **HLS** | **DASH** |
|---|---|---|---|
| Riproduzione generale (Riproduci, Pausa, Cerca) | VOD + Live | √ | Ö (solo VOD) |
| FER - Riproduzione generale (riproduzione, pausa, ricerca) | FER VOD | √ | Non supportato |
| MP3 | VOD | Non supportato | Non supportato |
| Riproduzione di contenuti MP4 | VOD | √ | √ |
| Logica di commutazione bitrate adattivo | VOD + Live | √ | Non supportato |
| Riproduzione solo audio | VOD + Live | √ | Non supportato |
| Sottotitoli codificati - 608/708 | VOD + Live | √ | Ö (solo VOD) |
| Sottotitoli codificati - WebVTT | VOD + Live | √ | Ö (solo VOD) |
| Failover manifesto | VOD + Live | √ | Ö (solo VOD) |
| Failover avanzato | VOD + Live | √ | Ö (solo VOD) |
| Notifiche QoS e del lettore | VOD + Live | √ | Ö (solo VOD) |
| Supporto per le intestazioni dei cookie | VOD + Live | √ | Ö (solo VOD) |
| Supporto per intestazioni personalizzate | VOD + Live | Non supportato | Non supportato |
| Impostare i parametri di controllo del buffer | VOD + Live | √ | Ö (solo VOD) |
| Impostare controlli bitrate adattivi | VOD + Live | √ | Ö (solo VOD) |
| Tag Manifest Personalizzati (HLS) / Flussi evento (DASH) | VOD + Live | √ | Ö (solo VOD) |
| Audio associato ritardato | VOD + Live | √ | Ö (solo VOD) |
| 302 Redirect | VOD + Live | √ | Ö (solo VOD) |

### Funzioni di riproduzione avanzate {#advanced-playback-features}

<table> 
 <tbody>
  <tr>
   <td><strong>Feature</strong></td> 
   <td><strong>Tipo di contenuto</strong></td> 
   <td><strong>HLS</strong></td> 
   <td><strong>DASH</strong></td> 
  </tr>
  <tr>
   <td>Riproduzione con offset</td> 
   <td>Live</td> 
   <td>√</td> 
   <td>Non supportato</td> 
  </tr>
  <tr>
   <td>Riproduzione solo audio</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>Non supportato</td> 
  </tr>
  <tr>
   <td>Gioco di mattoni </td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>Non supportato</td> 
  </tr>
  <tr>
   <td>Gioca a mattoni liscia (con ABR)</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>Non supportato</td> 
  </tr>
  <tr>
   <td>Analisi ID3 (HLS) / Metadati temporizzati (DASH)</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>Non supportato</td> 
  </tr>
  <tr>
   <td>Blackout </td> 
   <td>VOD + Live</td> 
   <td>Non supportato</td> 
   <td>Non supportato</td> 
  </tr>
  <tr>
   <td>Instant On</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>Non supportato</td> 
  </tr>
  <tr>
   <td>
    <ul> 
     <li>Supporto dei marcatori di discontinuità (HLS) </li> 
     <li>Più periodi (DASH)</li> 
    </ul> </td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>Non supportato</td> 
  </tr>
  <tr>
   <td>302 Disturbo di reindirizzamento</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>Ö (solo VOD)</td> 
  </tr>
  <tr>
   <td>Scorrimento miniature (Iframe e JPEG)</td> 
   <td>VOD + Live</td> 
   <td>Non supportato</td> 
   <td>Non supportato</td> 
  </tr>
  <tr>
   <td>Integrità flusso </td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>Non supportato</td> 
  </tr>
 </tbody>
</table>

### Funzioni di inserimento annunci core (CSAI) {#core-ad-insertion-features-csai}

| **Feature** | **Tipo di contenuto** | **HLS** | **DASH** |
|---|---|---|---|
| Riproduzione generale, annunci attivati | VOD + Live | √ | † (solo prerotoli VOD) |
| Contenuto FER con annunci abilitati | VOD | √ | Non supportato |
| Comportamenti annuncio predefiniti | VOD + Live | √ | † (solo prerotoli VOD) |
| VAST 2.0/3.0 | VOD + Live | √ | † (solo prerotoli VOD) |
| VMAP 1.0 | VOD + Live | √ | † (solo prerotoli VOD) |
| Annunci MP4 | VOD + Live | Ö (da CRS) | † (da CRS, solo prerotoli) |

### Funzioni avanzate di inserimento annunci (CSAI) {#advanced-ad-insertion-features-csai}

<table> 
 <tbody>
  <tr>
   <td><strong>Feature</strong></td> 
   <td><strong>Tipo di contenuto</strong></td> 
   <td><strong>HLS</strong></td> 
   <td><strong>DASH</strong></td> 
  </tr>
  <tr>
   <td>Gioco di mattoni con annunci attivati</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>Non supportato</td> 
  </tr>
  <tr>
   <td>Solo annunci </td> 
   <td>VOD</td> 
   <td>Non supportato</td> 
   <td>Non supportato</td> 
  </tr>
  <tr>
   <td>Parametri di targeting</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>† (solo prerotoli VOD)</td> 
  </tr>
  <tr>
   <td>Parametri personalizzati</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>† (solo prerotoli VOD)</td> 
  </tr>
  <tr>
   <td>Comportamenti annuncio personalizzati</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>† (solo prerotoli VOD)</td> 
  </tr>
  <tr>
   <td>Tag Ad Personalizzati</td> 
   <td>Live</td> 
   <td>√ </td> 
   <td>Non supportato</td> 
  </tr>
  <tr>
   <td>Risolutori annunci personalizzati</td> 
   <td>VOD + Live</td> 
   <td>√ </td> 
   <td>Non supportato</td> 
  </tr>
  <tr>
   <td>Risolutore annunci personalizzato a ruota libera</td> 
   <td>VOD</td> 
   <td>Non supportato</td> 
   <td>Non supportato</td> 
  </tr>
  <tr>
   <td>Sostituzione annunci C3 </td> 
   <td>VOD + Live</td> 
   <td>√ </td> 
   <td>Non supportato</td> 
  </tr>
  <tr>
   <td>Caricamento annuncio non aggiornato</td> 
   <td>VOD</td> 
   <td>√ </td> 
   <td>Non supportato</td> 
  </tr>
  <tr>
   <td>
    <ul> 
     <li>Supporto dei marcatori di discontinuità - SSAI (HLS) </li> 
     <li>Più periodi (DASH)</li> 
    </ul> </td> 
   <td>VOD + Live</td> 
   <td>√ </td> 
   <td> </td> 
  </tr>
  <tr>
   <td>Annunci per la compagnia, Annunci per banner e Annunci cliccabili</td> 
   <td>VOD + Live</td> 
   <td>√ </td> 
   <td>† (solo prerotoli VOD)</td> 
  </tr>
  <tr>
   <td>VPAID 2.0</td> 
   <td>VOD + Live</td> 
   <td>Ö (JS) </td> 
   <td>† (solo prerotoli VOD)</td> 
  </tr>
  <tr>
   <td>Uscita Annuncio Precoce</td> 
   <td>Live</td> 
   <td>√ </td> 
   <td>Non supportato</td> 
  </tr>
  <tr>
   <td>Creative VOD + priorità dal vivo basate su regole</td> 
   <td>VOD + Live</td> 
   <td>√ </td> 
   <td>Non supportato</td> 
  </tr>
  <tr>
   <td>Regole CRS </td> 
   <td>VOD + Live</td> 
   <td>√ </td> 
   <td>Non supportato</td> 
  </tr>
 </tbody>
</table>

## Funzioni di protezione dei contenuti {#content-protection-features}

| **Feature** | **Tipo di contenuto** | **HLS** | **DASH** |
|---|---|---|---|
| Crittografia AES | VOD + Live | √ | Ö (solo VOD) |
| Cifratura AES di esempio | VOD + Live | √ |  |
| Flussi token | VOD + Live | √ |  |
| DRM | VOD + Live | Solo DRM Primetime (futuro) Widevine) | Solo Widevine |
| Riproduzione esterna (RBOP) | VOD + Live | Solo Primetime DRM | Non supportato |
| Rotazione licenza | VOD + Live | Solo Primetime DRM | Non supportato |
| Rotazione chiave | VOD + Live | Solo Primetime DRM | Non supportato |

### Funzioni di integrazione {#integration-features}

| **Feature** | **Tipo di contenuto** | **HLS** | **DASH** |
|---|---|---|---|
| Integrazione VHL di Adobe Analytics | VOD + Live | √ | √ |
| Fatturazione | VOD + Live | √ | Non supportato |

## Funzioni non supportate {#features-not-supported}

Questa versione di TVSDK non supporta:

* Blackout degli annunci.
* Slow motion con il trucco.
* Cercate e riproducete i contenuti MP4.
* Inserimento di annunci con il contenuto principale MP4.
* Cerca quando viene riprodotto un annuncio.
* Riproduzione di annunci con supporti solo audio.

## Problemi noti e limitazioni {#known-issues-and-limitations}

Questa versione di TVSDK presenta i seguenti problemi:

* Arresto anomalo VOD DRM LBA per dispositivi specifici (Samsung Galaxy Tab 4) con audacia e clicca su annunci
* Post-roll non viene riprodotto per un contenuto specifico.
* L&#39;impostazione della didascalia di chiusura per le lingue CJK non funziona.
* Il video può uscire dalla modalità &quot;trucco&quot; automaticamente tra VOD e live.
* VHL: le chiamate heartbeat errate vengono inviate quando si avvia un contenuto da un offset.
* Quando gli annunci VPAID vengono riprodotti, le chiamate heartbeat VHL per event:type:play e gli annunci risultano mancanti.
* L&#39;annuncio pre-roll viene riprodotto anche quando viene selezionato lo SKIP adBreakPolicy.
* Dopo aver scelto il lettore di stato Complete, tornate allo stato di riproduzione con SKIP adBreakPolicy per gli annunci Post-roll.

Senza video, non esiste una dimensione di visualizzazione e senza una dimensione di visualizzazione non è possibile visualizzare alcuna grafica per le didascalie.

## Risorse utili {#helpful-resources}

* Consulta la documentazione completa della guida nella pagina Informazioni e supporto [di](https://helpx.adobe.com/support/primetime.html) Adobe Primetime.